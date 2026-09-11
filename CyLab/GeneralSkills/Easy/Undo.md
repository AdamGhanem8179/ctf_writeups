content = """# CyLab 2026 – Undo Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** Undo
* **Category:** General Skills / Cryptography
* **Points:** 100
* **Date:** 9/11/2026
* **Flag:** `picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_........}`

---

## TL;DR (Abstract)
The challenge applies a multi-step text transformation pipeline to obscure the original flag string. By analyzing the sequence of operations applied by the challenge instructions and systematically running the inverse operations in reverse order using standard Linux command-line utilities (such as `rev`, `base64 -d`, and `tr`), the transformations were completely undone to recover the original plaintext flag.

---

## Challenge Description
> Can you reverse the sequence of transformations? Follow the encoding trail backwards, undo each transformation with standard shell tools, and recover the hidden flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance & Analysis
Inspect the challenge file or prompt detailing the chain of transformations applied to the flag. Typical pipeline stages involve a sequence of reversible stream operations:

1. String reversal (`rev`)
2. Base64 encoding (`base64`)
3. Character substitution / translation (`tr`)

To reverse the transformation process, construct a pipeline applying the exact inverse operations in opposite order.
