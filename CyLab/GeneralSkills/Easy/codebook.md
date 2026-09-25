# picoCTF – Codebook Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Codebook

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{c0d3b00k_455157_........}

## TL;DR (Abstract)

The challenge provides a Python script (`code.py`) and an associated text file (`codebook.txt`). By running the script directly with Python 3 via `python3 code.py` in the same directory as the codebook file, the program reads the key data, decrypts the embedded ciphertext, and prints the flag to standard output.

## Challenge Description

> Run the Python script `code.py` in the same directory as `codebook.txt`.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge distributes two files in the working directory:

```bash
ls -la
```

Contents:
* `code.py` — The Python execution script.
* `codebook.txt` — The key/data file required during script execution.

Inspecting `code.py` shows that it requires `codebook.txt` to be present in the execution path to complete its routines and reveal the flag.

### 2. Execution & Flag Capture

Execute the Python script using the Python 3 interpreter:

```bash
python3 code.py
```

Terminal Output:

```
academy{c0d3b00k_455157_........}
```

The script processes the contents of `codebook.txt` and outputs the complete flag directly:

```
academy{c0d3b00k_455157_........}
```

## Remediation & Key Takeaways

* **Python Script Execution:** Python source files (`.py`) are interpreted directly using `python3 <script_name>.py` without needing a compilation step.
* **Working Directory Dependencies:** Scripts that use relative file paths (e.g., `open('codebook.txt')`) require the command to be executed from the directory where the dependent files reside.
