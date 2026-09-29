# CyLab – ASCII Numbers Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** ASCII Numbers

* **Category:** General Skills / Cryptography

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135\_........}

## TL;DR (Abstract)

The challenge presents a series of numerical values representing standard ASCII character byte codes. By parsing each numeric value and converting it back into its corresponding ASCII character using Python or command-line tools, the readable plaintext flag was recovered.

## Challenge Description

> Decode the provided series of ASCII numbers to recover the hidden flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the provided input:

* **Format:** A sequence of space-separated or array-formatted numeric values (decimal or hexadecimal byte codes).

* **Target:** Map each numeric value to its corresponding printable ASCII character.

### 2. ASCII Decoding

Standard printable characters map directly to integer values in the ASCII table (e.g., `97` for `'a'`, `123` for `'{'`, `125` for `'}'`).

Converting the sequence using Python:

```bash
python3 -c '
nums = [...] # numeric sequence provided by challenge
print("".join(chr(int(n, 0) if isinstance(n, str) else n) for n in nums))
'
```

Alternatively, converting hexadecimal byte strings using Linux utilities:

```bash
echo "0x61 0x63 0x61 0x64 0x65 0x6d 0x79" | tr -d '0x' | tr -d ' ' | xxd -r -p
```

### 3. Execution & Flag Capture

Evaluating all numerical codes yields the decoded flag string:

```text
academy{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_........}
```

Flag:

```text
academy{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_........}
```
