# picoCTF – fixme2.py Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** fixme2.py

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{3qu4l1ty_n0t_4551gnm3nt_........}

## TL;DR (Abstract)

The challenge provides a Python script (`fixme2.py`) containing a syntax error caused by using the assignment operator (`=`) inside an `if` condition instead of the equality comparison operator (`==`). Correcting the operator to `==` resolves the `SyntaxError` and allows the script to decrypt and print the flag.

## Challenge Description

> Fix the syntax error in the Python script to inspect the code and get the flag.
> Download Python code `fixme2.py`.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Running the supplied Python script directly with the interpreter results in an immediate failure before runtime execution:

```bash
python3 fixme2.py
```

Output:

```text
  File "/home/user/fixme2.py", line 22
    if flag = "":
            ^
SyntaxError: invalid syntax. Maybe you meant '==' or ':='?
```

The Python interpreter flags an invalid syntax error located at line 22 within an `if` statement.

### 2. Code Inspection & Bug Analysis

Inspecting line 22 of `fixme2.py`:

```python
# Check that flag is not empty
if flag = "":
  print('That defines an empty string, please run with the flag as argument.')
else:
  # Decrypt and print flag logic follows...
```

* In Python, a single equals sign (`=`) is the **assignment operator**, used to bind a variable name to a value.
* Conditional checks require a comparison operator; equality evaluation is performed using double equals (`==`).
* Placing an assignment statement inside a standard `if` conditional violates Python's syntax rules, preventing the script from compiling.

### 3. Execution & Flag Capture

Open `fixme2.py` in a text editor (e.g., `nano`, `vim`, or VS Code) and update the comparison operator on line 22:

```python
# Before
if flag = "":

# After
if flag == "":
```

Save the file and execute the script again:

```bash
python3 fixme2.py
```

Terminal Output:

```text
That is correct! Here's your flag: academy{3qu4l1ty_n0t_4551gnm3nt_........}
```

The script successfully evaluates the condition, completes the XOR decryption routine, and outputs the flag:

```
academy{3qu4l1ty_n0t_4551gnm3nt_........}
```

## Remediation & Key Takeaways

* **Equality vs. Assignment:** In almost all C-style and high-level languages, `=` assigns a value to a memory location, whereas `==` evaluates value equality between two operands.
* **Interpreter Feedback:** Modern Python (3.10+) provides precise syntax suggestions in tracebacks (e.g., `Maybe you meant '==' or ':='?`), pinpointing the exact column and token responsible for the parsing failure.
* **Static Analysis:** Running linters such as `flake8` or `pylint` catches invalid syntax and logical assignment-in-conditional errors prior to code execution.
