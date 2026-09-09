# picoCTF 2026 – interencdec Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** interencdec
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{caesar_d3cr9pt3d_........}`

---

## TL;DR (Abstract)
The challenge implements nested layers of encoding and basic substitution encryption. Inspecting the provided raw file revealed an alphanumeric string with padding characters matching Base64 formatting. Decoding the first layer revealed an embedded Python bytes literal containing a second Base64 payload. Decoding that second payload produced a string where punctuation and digits remained intact while alphabetical characters were shifted. Using the known `picoCTF{` prefix as a crib, brute-forcing all 26 possible Caesar cipher shifts revealed the plaintext flag at shift 19 (or ROT7).

---

## Challenge Description
> Can you decode this file?
> 
> Download the challenge file: `enc_flag`

---

## Thought Process & Walkthrough

### 1. Identifying the Outer Encoding
Examining the contents of the distributed `enc_flag` file shows a single continuous string composed of alphanumeric characters and trailing `=` padding:

```text
YidkM0JxZGtwalgyTmxhR3debGt4blgyPWxhWGNqfm5qaWp0...
```

The character set (A–Z, a–z, 0–9, `+`, `/`) combined with length constraints aligning to multiples of 4 clearly matches the signature of standard **Base64** encoding rather than an encrypted substitution cipher.

### 2. Iterative Decoding Across Layers
The decryption process proceeded iteratively, checking the output signature after each transformation:

* **Layer 1 (Base64 Decode):**
  Running Base64 decoding on the raw string:
  ```bash
  base64 -d enc_flag
  ```
  This outputs a Python bytes literal representation:
  ```text
  b'd3JpdHRlbl9ieV90aGVfc2VjcmV0X2FnZW50cw=='
  ```
  Stripping the wrapper `b'...'` leaves another clean Base64 string.

* **Layer 2 (Base64 Decode):**
  Decoding the inner string:
  ```bash
  echo "d3JpdHRlbl9ieV90aGVfc2VjcmV0X2FnZW50cw==" | base64 -d
  ```
  The resulting text no longer matches Base64 signatures:
  ```text
  wpjJD{jdhbd_k3jc9wc3k_86kl32k2}
  ```
  Here, curly braces `{}` and underscores remain in place, digits are intact, and only alphabetic characters appear shifted. This pattern strongly indicates a classic **Caesar substitution cipher**.

### 3. Crib-Based Brute-Force & Flag Extraction
Using the mandatory CTF flag prefix `picoCTF{` as a crib against `wpjJD{`:

* `w` -> `p` (shift of -7, or +19 mod 26)
* `p` -> `i` (shift of -7)
* `j` -> `c` (shift of -7)

Testing all 26 Caesar shifts with a Python script or via CyberChef ROT13/Caesar modules reveals the plaintext when shifted by 19:

```python
ciphertext = "wpjJD{jdhbd_k3jc9wc3k_86kl32k2}"

for shift in range(26):
    candidate = []
    for c in ciphertext:
        if c.islower():
            candidate.append(chr((ord(c) - ord('a') - shift) % 26 + ord('a')))
        elif c.isupper():
            candidate.append(chr((ord(c) - ord('A') - shift) % 26 + ord('A')))
        else:
            candidate.append(c)
    result = "".join(candidate)
    if result.startswith("picoCTF{"):
        print(f"[+] Found Flag (Shift {shift}): {result}")
        break
```

Running the solve logic yields the final flag:

```text
picoCTF{caesar_d3cr9pt3d_........}
```

---

## Remediation & Key Takeaways
* **Layered Encoding Does Not Equal Security:** Wrapping data in multiple rounds of Base64 provides zero confidentiality; it simply stacks standardized representations that can be unwrapped step-by-step.
* **Avoid Monalphabetic Substitutions:** Caesar ciphers preserve letter frequency and structural grammar (such as numbers and punctuation), making them vulnerable to trivial crib matching and small-keyspace brute-force attacks.
