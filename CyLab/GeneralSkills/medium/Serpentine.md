# CyLab – Serpentine Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Serpentine

* **Category:** Reverse Engineering / Python

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{7h3_r04d_l355_7r4v3l3d_........}

## TL;DR (Abstract)

The challenge provides a Python script named `serpentine.py` featuring an interactive menu interface. Inspecting the code reveals an unreferenced `print_flag()` function. By invoking the script in interactive mode using `python3 -i`, exiting the menu loop leaves the Python runtime active with the script's global scope accessible, allowing direct invocation of `print_flag()` to recover the flag without modifying the source file.

## Challenge Description

> Find the flag hidden within the provided `serpentine.py` script.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the source code of `serpentine.py`:

* **Interface:** An interactive text menu loop presenting several user options (e.g., printing random facts or quitting).
* **Target Function:** A helper function named `print_flag()` is defined within the script:
  ```python
  def print_flag():
      # Flag decryption and printing logic
      ...
  ```
* **Vulnerability / Flow Flaw:** None of the menu branches call `print_flag()`. However, the function exists in the global namespace.

### 2. Execution via Interactive Mode (`-i`)

Running a script with Python's `-i` flag forces the interpreter into interactive mode after execution finishes, keeping all defined objects and functions loaded in memory.

1. Launch `serpentine.py` with the interactive flag:
   ```bash
   python3 -i serpentine.py
   ```

2. When prompted by the menu, choose option `c` (or exit the loop):
   * This drops the session directly into the active Python shell prompt (`>>>`).

3. Call the hidden function directly from the interpreter:
   ```python
   >>> print_flag()
   ```

### 3. Alternative Approaches

* **Source Code Patching:** Edit `serpentine.py` with `nano` or `vim` to call `print_flag()` directly within the menu handler:
  ```python
  elif choice == 'b':
      print_flag()
  ```
* **One-liner Execution:** Import the module directly from the command line:
  ```bash
  python3 -c "import serpentine; serpentine.print_flag()"
  ```

### 4. Execution & Flag Capture

Invoking `print_flag()` prints the reconstructed plaintext flag:

```text
academy{7h3_r04d_l355_7r4v3l3d_........}
```

Flag:

```text
academy{7h3_r04d_l355_7r4v3l3d_........}
```
