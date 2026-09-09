# picoCTF 2026 – hashcrack

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** Weak Hashes
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{UseStr0nG_h@shEs_&PaSswDs!_........}`

---

## TL;DR (Abstract)
The challenge demonstrates the critical danger of storing passwords using fast, unsalted cryptographic hash functions. Connecting to the target TCP service presents a multi-stage authentication challenge requiring reverse-engineering password digests. By analyzing hash output lengths and character sets, the digests were mapped to standard MD5, SHA-1, and SHA-256 algorithms. Running straight dictionary attacks with hashcat against rockyou.txt successfully cracked all three plaintexts in sequence, yielding the flag upon submitting the final recovered password over netcat.

---

## Challenge Description
> A company stored a secret message on a server which got breached due to the admin using weakly hashed passwords. Can you gain access to the secret stored within the server?
> 
> Connect to the instance:
> `nc verbal-sleep.picoctf.net 49505`

---

## Thought Process & Walkthrough

### 1. Hash Algorithm Identification
Connecting to the challenge server prompts for the plaintext password corresponding to an initial digest. Analyzing the length and character set of the provided digests across the stages reveals their respective algorithms:

* **Stage 1:** 32 hexadecimal characters (128 bits) -> **MD5** (`hashcat -m 0`)
* **Stage 2:** 40 hexadecimal characters (160 bits) -> **SHA-1** (`hashcat -m 100`)
* **Stage 3:** 64 hexadecimal characters (256 bits) -> **SHA-256** (`hashcat -m 1400`)

The algorithm types were verified using hashcat's identification utilities:
```bash
hashcat --identify hash.txt
```
The challenge description highlights that the administrator used "weakly hashed passwords", confirming that no salt, key stretching, or custom HMAC wrappers were applied to the digests.

### 2. Dictionary Attacks with Hashcat
With the algorithms determined to be raw unsalted digests, dictionary attacks (`-a 0`) were executed sequentially against the standard `rockyou.txt` wordlist.

* **Stage 1 (MD5):**
```bash
hashcat -m 0 -a 0 hash_stage1.txt rockyou.txt
```
Result recovered: `password123`

* **Stage 2 (SHA-1):**
```bash
hashcat -m 100 -a 0 hash_stage2.txt rockyou.txt
```
Result recovered: `letmein`

* **Stage 3 (SHA-256):**
```bash
hashcat -m 1400 -a 0 hash_stage3.txt /usr/share/wordlists/rockyou.txt
```
While a short custom wordlist failed to match the digest, escalating to the complete 14.3M-entry `rockyou.txt` dictionary cracked the hash successfully.
Result recovered: `qwerty098`

### 3. Verification & Flag Capture
Before sending the inputs over the network socket, each plaintext candidate was verified locally to ensure the recomputed digest matched the server prompt:

```bash
echo -n "password123" | md5sum
echo -n "letmein" | sha1sum
echo -n "qwerty098" | sha256sum
```

Connect back to the challenge instance using `nc` and submit the cracked plaintexts sequentially:

```bash
nc verbal-sleep.picoctf.net 49505
```

Feeding `password123`, `letmein`, and `qwerty098` into their corresponding stage prompts unlocked the server secret and revealed the flag:

```text
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_........}
```

---

## Remediation & Key Takeaways
* **Avoid General-Purpose Hash Functions for Passwords:** Algorithms like MD5, SHA-1, and SHA-256 are engineered for speed, making them exceptionally vulnerable to high-throughput GPU cracking attacks.
* **Use Modern Key Derivation Functions:** Store password credentials using slow, memory-hard hashing algorithms such as Argon2id, bcrypt, or scrypt.
* **Enforce Per-User Unique Salts:** Cryptographic salts prevent precomputed dictionary and rainbow table lookups, ensuring identical passwords generate distinct stored hashes.
