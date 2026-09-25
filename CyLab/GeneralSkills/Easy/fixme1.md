# picoCTF – fixme1.py Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** fixme1.py

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{1nd3nt1ty_cr1515_........}

## TL;DR (Abstract)

The challenge provides a Python script (`fixme1.py`) that fails to run due to an `IndentationError`. Inspecting the source shows that the final `print()` statement contains unexpected leading whitespace. Removing the extraneous indentation and executing the script using `python3 fixme1.py` successfully runs the decryption logic and outputs the flag.

## Challenge Description

> Fix the syntax error in this Python script to print the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Attempting to run the script immediately with the Python 3 interpreter:

```
python3 fixme1.py
```

The interpreter throws a syntax exception and halts execution:

```
  File "fixme1.py", line 20
    print('That is correct! Here\'s your flag: ' + flag)
IndentationError: unexpected indent
```

### 2. Identifying the Bug

Inspecting the bottom lines of `fixme1.py`:

```python
flag = str_xor(flag_enc, 'bonkers')
  print('That is correct! Here\'s your flag: ' + flag)
```

The final `print()` call contains leading spaces, placing it out of alignment with the preceding module-level code block. In Python, module-level statements must not have leading indentation.

### 3. Execution & Flag Capture

Edit `fixme1.py` with a text editor (`nano fixme1.py` or `vim fixme1.py`) and delete the two leading spaces on line 20:

```python
flag = str_xor(flag_enc, 'bonkers')
print('That is correct! Here\'s your flag: ' + flag)
```

Save the file and run it:

```
python3 fixme1.py
```

Terminal Output:

```
That is correct! Here's your flag: academy{1nd3nt1ty_cr1515_........}
```

This yields the complete flag:

```
academy{1nd3nt1ty_cr1515_........}
```

## Remediation & Key Takeaways

* **Python Indentation Syntax:** Python uses indentation levels to denote scope rather than explicit block delimiters like `{}`. Extraneous or inconsistent spaces trigger an immediate `IndentationError`.
* **Interpreting Tracebacks:** Python stack traces provide the exact file name and offending line number (`line 20`), allowing swift triage and patching of syntax bugs.
