# picoCTF – runme.py Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** runme.py

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{run_s4n1ty_...}

## TL;DR (Abstract)

The challenge provides a standalone Python script named `runme.py`. The objective is to execute the file within a Python runtime environment using the command-line interpreter. Running `python3 runme.py` executes the script's internal logic, which decrypts and prints the flag directly to standard output.

## Challenge Description

> Run the `runme.py` script to get the flag. Download the script with your browser or with `wget` in the webshell.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

After obtaining the file via direct download or through the terminal using `wget`:

```bash
wget <challenge-url>/runme.py
```

Check the file attributes using the `file` utility to confirm its format:

```bash
file runme.py
```

Output:

```text
runme.py: Python script, ASCII text executable
```

The file is a standard, uncompiled ASCII text Python script.

### 2. Code Inspection (Optional)

Inspecting the script's contents using `cat` reveals how the flag is handled:

```bash
cat runme.py
```

The script defines an obfuscated flag string and a decoding function, then invokes `print()` to reveal the flag upon execution:

```python
# Sample snippet from runme.py structure
flag = '...'
print(decode_flag(flag))
```

Because the script does not require interactive input or argument passing, executing it directly via the Python 3 interpreter is sufficient.

### 3. Execution & Flag Capture

Execute the script from the directory containing `runme.py` using `python3`:

```bash
python3 runme.py
```

Terminal Output:

```text
academy{run_s4n1ty_...}
```

The script completes execution immediately and prints the final flag:

```
academy{run_s4n1ty_...}
```

## Remediation & Key Takeaways

* **Interpreter Invocations:** In Linux environments, Python scripts are invoked by passing the filename as an argument to the interpreter (`python3 script.py`) or by granting execute permissions (`chmod +x script.py`) if a shebang line (e.g., `#!/usr/bin/env python3`) is present at the top of the file.
* **Basic Source Inspection:** Viewing script contents with CLI pagers (`cat`, `less`, `bat`) before running third-party scripts ensures safety and confirms program behavior.
