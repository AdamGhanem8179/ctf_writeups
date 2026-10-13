# CyLab – Python Wrangling Write-up

## Step 0 - Challenge Info

- **CTF Name:** CyLab
- **Challenge Name:** Python Wrangling
- **Category:** General Skills
- **Points:** 50
- **Date:** 10/13/2026
- **Flag:** academy{4p0110_1n_7h3_h0us3_.........}

## TL;DR (Abstract)

The challenge provides a Python script (`ende.py`) designed to encrypt and decrypt files, an encrypted flag file (`flag.txt.en`), and a text file containing a password (`password.txt`). By running the Python script in decryption mode and supplying the provided password, the script decodes the ciphertext and outputs the plaintext flag.

## Challenge Description

> Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the provided files downloaded from the challenge:

- `ende.py`: A Python script that handles symmetric encryption and decryption. Looking at the help menu or the code reveals it accepts arguments like `-e` (encrypt) and `-d` (decrypt).
- `flag.txt.en`: The target file containing the encrypted flag ciphertext.
- `password.txt`: Contains the plaintext password required by `ende.py` to derive the decryption key. 

First, we read the password from the text file so it is ready to be pasted when prompted.

### 2. Execution & Decryption

To decrypt the file, the Python script must be executed via the command line using the `-d` flag, followed by the target encrypted file.

```bash
python3 ende.py -d flag.txt.en
```

Upon execution, the script prompts the user for the password. Inputting the exact string found in `password.txt` successfully authenticates the decryption routine.

Output:

```text
Please enter the password: *****************
academy{4p0110_1n_7h3_h0us3_.........}
```

### 3. Flag Capture

The script successfully decrypts the ciphertext and prints the flag to standard output. 

Flag:

```text
academy{4p0110_1n_7h3_h0us3_.........}
```
