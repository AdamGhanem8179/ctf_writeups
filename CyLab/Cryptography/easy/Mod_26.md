# picoCTF 2026 – Mod 26 Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** Mod 26
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{next_time_I'll_try_2_rounds_of_rot13_........}`

---

## TL;DR (Abstract)
The challenge hints at modular arithmetic over the Latin alphabet through its title, "Mod 26". The challenge description provides an encrypted string following the standard CTF flag format. Recognizing the mathematical reference to a Caesar shift of 13 positions ($C \equiv P + 13 \pmod{26}$), pasting the ciphertext directly into an online ROT13 decoder inverted the substitution and yielded the plaintext flag.

---

## Challenge Description
> Cryptography can be easy, do you know what ROT13 is?
> 
> `cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_n5813542}`

---

## Thought Process & Walkthrough

### 1. Analyzing the Title & Ciphertext
The challenge title "Mod 26" directly references modulo 26 arithmetic, which is the foundational mathematical operation for Caesar ciphers operating on the 26-letter English alphabet.

Looking at the provided ciphertext:
```text
cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_n5813542}
```

The string clearly shows the standard flag wrapper structure. The prefix `cvpbPGS` shifts directly to `picoCTF` when rotated by 13 positions:
* `c` (+13) -> `p`
* `v` (+13) -> `i`
* `p` (+13) -> `c`
* `b` (+13) -> `o`
* `P` (+13) -> `C`
* `G` (+13) -> `T`
* `S` (+13) -> `F`

Because applying ROT13 twice completes a full 26-position cycle, running the ROT13 algorithm on the ciphertext reverses the encryption and reveals the plaintext.

### 2. Decoding & Flag Retrieval
To decode the string:

1. Open an online ROT13 decoder (such as rot13.com or CyberChef).
2. Paste the ciphertext into the input box:
   ```text
   cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_n5813542}
   ```
3. Read the decoded plaintext result:
   ```text
   picoCTF{next_time_I'll_try_2_rounds_of_rot13_a5813542}
   ```

Alternatively, decode it directly in the Linux terminal using `tr`:
```bash
echo "cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_n5813542}" | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Final flag:
```text
picoCTF{next_time_I'll_try_2_rounds_of_rot13_........}
```

---

## Remediation & Key Takeaways
* **ROT13 Offers No Confidentiality:** ROT13 is a reciprocal cipher with a fixed key ($k = 13$). It cannot protect sensitive information against unauthorized decryption.
* **Modular Arithmetic Weakness:** Any simple additive cipher ($P + k \pmod{26}$) has an extremely small key space of only 25 possible variations, rendering it completely trivial to brute-force or detect.
