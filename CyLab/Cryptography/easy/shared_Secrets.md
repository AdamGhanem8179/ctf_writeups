# picoCTF 2026 – Shared Secrets Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** Shared Secrets
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{dh_s3cr3t_........}`

---

## TL;DR (Abstract)
The challenge implements a standard Diffie-Hellman Key Exchange combined with symmetric single-byte XOR encryption. Inspecting the provided source code and transmission leaks revealed the public parameters ($g$, $p$), Alice's public key ($A$), the ciphertext bytes, and crucially, Bob's private exponent ($b$). Because Bob's private key was directly leaked, the shared secret was immediately computable via modular exponentiation ($S \equiv A^b \pmod p$). Deriving the single-byte keystream via $S \pmod{256}$ and XORing against the ciphertext recovered the flag.

---

## Challenge Description
> A message was encrypted using a shared secret... but it looks like one side of the exchange leaked something. Can you piece together the secret and get the flag?

---

## Thought Process & Walkthrough

### 1. Code & Leak Analysis
Reviewing the challenge distribution files reveals a standard Diffie-Hellman Key Exchange (DHKE) implementation. In Diffie-Hellman:

* Alice generates private key $a$ and calculates $A = g^a \pmod p$.
* Bob generates private key $b$ and calculates $B = g^b \pmod p$.
* The shared secret is derived as:
  $$S = B^a \equiv (g^b)^a \equiv g^{ab} \equiv (g^a)^b \equiv A^b \pmod p$$

Under normal circumstances, an eavesdropper only sees $g$, $p$, $A$, and $B$, requiring the computationally infeasible Discrete Logarithm Problem (DLP) to break. However, inspecting the leaked files reveals that one participant accidentally exposed their private key: Bob's private exponent $b$ is completely known.

Along with $b$, we are provided:
* The generator $g = 2$
* The prime modulus $p$
* Alice's public component $A$
* The encrypted hex string `cfd6dcd0...`

The encryption mechanism computes the shared secret $S$, extracts a key byte via $S \pmod{256}$, and performs a byte-by-byte XOR against the plaintext.

### 2. Deriving the Shared Secret
With Alice's public key $A$ and Bob's private key $b$ in hand, no discrete logarithm attack is necessary. We compute the shared secret directly:

$$S = A^b \pmod p$$

Python handles large arbitrary-precision integers natively with built-in modular exponentiation:
```python
shared = pow(A, b, p)
```

### 3. Decryption Script & Flag Retrieval
Once $S$ is calculated, we take `shared % 256` to derive the single-byte XOR key and decrypt the hex-encoded ciphertext.

```python
g = 2
p = 1653798930689987750372209240014380521131540183716217687164747711336243702962818359267822691525697642105558753651223568056089606926425342081267821725904109431430327153613733358950243154522848602494020618427146508586350079988809469424456886589329449769221123659126892760967096413248127035734431548987006011015808526671
A = 771122236020803078829911570090382183223626843114693013412703353349864301811612864849857638111588507084769437566078749825291937213523446695097948166153379036322108656350710200734137906115055446496743841090323252143278700024424965369059879247648625799137192258413471893876530475007392243768366999108564494255853654467
b = 502087552249276796768894199149546386713173741864561762918671131549146319658647813949433247424965048798816294966029262647803764533595143429273283374211302160540685383641060542870573303301014875733971557824236009184578986290165659257363419797500816452080900496604781986251988455903195756181696996025184087945715324970
enc_hex = "cfd6dcd0fcebf9c4dbd7e0cc8cdccd8ccbe0dddb8c87d98c8889c2"

# Compute the shared secret using leaked private key b and public key A
shared = pow(A, b, p)

# Extract 1-byte key and decrypt XOR ciphertext
enc = bytes.fromhex(enc_hex)
key_byte = shared % 256
flag = bytes(x ^ key_byte for x in enc)

print("flag =", flag.decode())
```

Running the solve script decrypts the ciphertext into ASCII and yields the flag:

```text
picoCTF{dh_s3cr3t_........}
```

---

## Remediation & Key Takeaways
* **Protect Ephemeral Private Keys:** Diffie-Hellman relies completely on the confidentiality of private exponents ($a$ and $b$). Leaking either value destroys the forward secrecy and confidentiality guarantees of the exchange.
* **Proper Key Derivation Functions (KDF):** Never truncate or modulo a shared secret down to a single byte ($S \pmod{256}$) for encryption. Use standard KDFs (such as HKDF-SHA256) to derive robust, full-length keys for authenticated ciphers like AES-GCM.
