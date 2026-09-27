# CyLab – PW Crack 4 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** PW Crack 4

* **Category:** General Skills / Reverse Engineering

* **Points:** 50

* **Date:** 9/27/2026

* **Flag:** academy{fl45h_5pr1ng1ng_........}

## TL;DR (Abstract)

The challenge builds on the previous level by expanding the candidate password pool to a list of 100 possible values inside `level4.py`. By scripting an automated Python loop with `hashlib` to compute the MD5 digest of each entry in `pos_pw_list` and compare it against `level4.hash.bin`, the valid password was rapidly identified and supplied to decrypt and display the flag.

## Challenge Description

> Can you crack the password to get the flag? Download the password checker script and encrypted flag file.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the challenge files in the directory:

* `level4.py`: The password verification and decryption script containing a 100-item array (`pos_pw_list`).
* `level4.hash.bin`: A binary file storing the target MD5 hash digest.
* `level4.flag.txt.enc`: The XOR-encrypted flag data.

Because manual entry of 100 candidate strings via the CLI prompt is slow and error-prone, an automated hash-matching script was constructed.

### 2. Scripting the Solution

A Python script was written to iterate over each entry in `pos_pw_list`, hash it using MD5, and test it against the binary contents of `level4.hash.bin`:

```python
import hashlib

def hash_pw(pw_str):
    m = hashlib.md5()
    m.update(pw_str.encode())
    return m.digest()

with open('level4.hash.bin', 'rb') as f:
    correct_pw_hash = f.read()

pos_pw_list = [
    "8c86", "7692", "a519", "3e61", "7dd6", "8919", "aaea", "f34b",
    "d9a2", "39f7", "626b", "dc78", "2a98", ...
]

for pw in pos_pw_list:
    if hash_pw(pw) == correct_pw_hash:
        print("Password is:", pw)
        break
```

Running this solver identifies the matching plaintext password directly.

### 3. Execution & Flag Capture

Execute `level4.py` and submit the recovered password at the prompt:

```bash
python3 level4.py
```

Terminal Interaction:

```text
Please enter correct password for flag: [cracked_password]
Welcome back... your flag, user:
academy{fl45h_5pr1ng1ng_........}
```

Flag:

```
academy{fl45h_5pr1ng1ng_........}
```
