# CyLab – PW Crack 5 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** PW Crack 5

* **Category:** General Skills / Reverse Engineering

* **Points:** 50

* **Date:** 9/28/2026

* **Flag:** academy{h45h_sl1ng1ng_........}

## TL;DR (Abstract)

The final installment of the PW Crack series replaces an inline candidate list with an external dictionary file (`dictionary.txt`) containing thousands of potential passwords. By designing a custom automated script to read through the dictionary entries line by line, hash each candidate, and compare the digests against `level5.hash.bin`, the matching password was identified and used to execute `level5.py` and print the flag.

## Challenge Description

> Can you crack the password to get the flag? Download the password checker script, encrypted flag file, and dictionary file.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the files provided for the challenge:

* `level5.py`: The password verification and XOR decryption script.
* `level5.hash.bin`: The raw MD5 hash of the correct password.
* `level5.flag.txt.enc`: The encrypted flag file.
* `dictionary.txt`: A comprehensive wordlist of candidate passwords.

Unlike previous levels where candidates were hardcoded inside the script, this challenge scales the search space significantly by requiring the program to read from an external dictionary.

### 2. Strategy & Wordlist Cracking

To uncover the password:

1. Parse the binary digest stored inside `level5.hash.bin`.
2. Stream and process each line from `dictionary.txt`.
3. Compute the cryptographic hash for each entry and cross-reference it against the binary target digest until an identical match is found.
4. Output the discovered password string.

*(Custom cracking script omitted to prevent unauthorized reuse).*

### 3. Execution & Flag Capture

Execute `level5.py` and input the recovered password at the prompt:

```bash
python3 level5.py
```

Terminal Interaction:

```text
Please enter correct password for flag: [REDACTED]
Welcome back... your flag, user:
academy{h45h_sl1ng1ng_........}
```

Flag:

```
academy{h45h_sl1ng1ng_........}
```
