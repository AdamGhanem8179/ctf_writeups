# picoCTF 2026 – EVEN RSA CAN BE BROKEN??? Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** EVEN RSA CAN BE BROKEN???
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{tw0_1$_............}`

---

## TL;DR (Abstract)
The challenge presents an RSA implementation vulnerable to trivial modulus factorization. Inspecting the public modulus $N$ revealed that it was an even integer, violating the fundamental RSA constraint that both prime factors must be odd primes. Because $2 \mid N$, the prime factors were immediately known as $p = 2$ and $q = N // 2$. Euler's totient was trivially computed as $\phi(N) = (2 - 1)(q - 1) = q - 1$, allowing the derivation of the private exponent $d \equiv e^{-1} \pmod{\phi(N)}$. Decrypting the ciphertext via modular exponentiation successfully revealed the flag.

---

## Challenge Description
> EVEN RSA CAN BE BROKEN???
> 
> Can you decrypt this message?
> Files provided: `output.txt` (containing $N$, $e$, and $c$)

---

## Thought Process & Walkthrough

### 1. Modulus Parity Inspection
In standard RSA, the modulus $N$ is the product of two distinct, large odd primes ($N = p \times q$). 

Examining the modulus $N$ provided in the challenge output file:
* The last digit of $N$ was even.
* Therefore, $N \equiv 0 \pmod 2$, meaning $2 \mid N$.

Since 2 is the only even prime number, having an even modulus guarantees that one of the secret prime factors was set to $p = 2$.

### 2. Factoring N & Deriving the Private Key
Because $p = 2$, factoring $N$ requires no advanced algorithms (such as ECM or Pollard's $p-1$):

$$q = \frac{N}{2}$$

Euler's totient function $\phi(N)$ for two distinct primes is given by:

$$\phi(N) = (p - 1)(q - 1) = (2 - 1)(q - 1) = q - 1$$

With $\phi(N)$ known, the private decryption exponent $d$ is derived as the modular inverse of the public exponent $e$:

$$d \equiv e^{-1} \pmod{\phi(N)}$$

### 3. Decryption Script & Flag Recovery
The complete mathematical recovery was executed via a short Python script:

```python
from Crypto.Util.number import long_to_bytes

# Given challenge parameters
N = ... # Even modulus from output.txt
e = 65537
c = ... # Ciphertext from output.txt

# Factor modulus trivially
p = 2
q = N // 2

# Calculate totient
phi = (p - 1) * (q - 1)  # Equals q - 1

# Compute private key d
d = pow(e, -1, phi)

# Decrypt ciphertext
m = pow(c, d, N)

# Convert integer to ASCII plaintext
flag = long_to_bytes(m)
print(flag.decode())
```

Running the solve script outputs the decrypted flag:

```text
picoCTF{tw0_1$_.............}
```

---

## Remediation & Key Takeaways
* **Strict Prime Generation:** Primes selected for RSA must be cryptographically secure, random, and sufficiently large (e.g., minimum 2048-bit total modulus size).
* **Parity Validation:** Using small primes—especially $p = 2$—completely collapses RSA security down to a single division operation.
