# CyLab – PW Crack 2 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** PW Crack 2

* **Category:** General Skills / Reverse Engineering

* **Points:** 50

* **Date:** 9/26/2026

* **Flag:** academy{tr45h_51ng1ng_........}

## TL;DR (Abstract)

The challenge provides a password-protected script where the correct password is obfuscated using hexadecimal ASCII character codes via `chr(...)`. Inspecting the script source code revealed this comparison condition. By decoding the hex character sequence in Python, the plaintext password was recovered, and entering it into the program unlocked the flag.

## Challenge Description

> Can you crack the password to get the flag? Download the password checker script and encrypted flag file.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the source code of the challenge script using `cat`:

```bash
cat level2.py
```

Reading through the source reveals that the password comparison no longer checks against a plain text string literal, but instead compares user input against evaluated ASCII byte values:

```python
user_pw = input("Please enter correct password for flag: ")
if user_pw == chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36):
    print("Welcome back... your flag, user:")
    decryption = str_xor(flag_enc.decode(), user_pw)
    print(decryption)
```

### 2. Password Decoding

Decode the ASCII hexadecimal values using a one-line Python command:

```bash
python3 -c "print(chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36))"
```

Terminal Output:

```text
de76
```

The reconstructed password is `de76`.

### 3. Execution & Flag Capture

Execute `level2.py` and supply `de76` when prompted:

```bash
python3 level2.py
```

Terminal Interaction:

```text
Please enter correct password for flag: de76
Welcome back... your flag, user:
academy{tr45h_51ng1ng_........}
```

Flag:

```
academy{tr45h_51ng1ng_........}
```
