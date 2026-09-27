# CyLab – PW Crack 3 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** PW Crack 3

* **Category:** General Skills / Reverse Engineering

* **Points:** 50

* **Date:** 9/27/2026

* **Flag:** academy{m45h_fl1ng1ng_........}

## TL;DR (Abstract)

The challenge presents a Python script that validates input against an MD5 password hash rather than checking plain text directly. Inside the source code, a limited array of candidate password strings is defined. By evaluating the candidate list against the target hash, the valid password was identified and submitted to unlock and decrypt the flag.

## Challenge Description

> Can you crack the password to get the flag? Download the password checker script and encrypted flag file.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the source code of the script using `cat`:

```bash
cat level3.py
```

Inside the file, the password validation logic uses MD5 hashing to verify user input against a binary hash file (`level3.hash.bin`), alongside a predefined list of 7 candidate password possibilities:

```python
pos_pw_list = ["8799", "d3ab", "1ea2", "ac25", "cd1e", "2b98", "5479"]
correct_pw_hash = open('level3.hash.bin', 'rb').read()

def check_password():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
```

### 2. Candidate Analysis & Cracking

Instead of manual guessing, iterate through the candidates in `pos_pw_list` by hashing each string and matching it against `correct_pw_hash`:

```bash
python3 -c '
import hashlib
target = open("level3.hash.bin", "rb").read()
for pw in ["8799", "d3ab", "1ea2", "ac25", "cd1e", "2b98", "5479"]:
    if hashlib.md5(pw.encode()).digest() == target:
        print(f"Password found: {pw}")
        break
'
```

### 3. Execution & Flag Capture

Execute `level3.py` and supply the identified matching password when prompted:

```bash
python3 level3.py
```

Terminal Interaction:

```text
Please enter correct password for flag: <matching_password>
Welcome back... your flag, user:
academy{m45h_fl1ng1ng_........}
```

Flag:

```
academy{m45h_fl1ng1ng_........}
```
