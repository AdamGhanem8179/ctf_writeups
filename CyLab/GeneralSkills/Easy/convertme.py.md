# picoCTF – convertme.py Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** convertme.py

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{4ll_y0ur_b4535_........}

## TL;DR (Abstract)

The challenge provides a Python script (`convertme.py`) that presents a decimal number and asks for its binary representation. By running the script via `python3 convertme.py`, calculating the binary equivalent using a terminal one-liner or manual division, and entering the resulting string, the script verifies the answer and prints the flag.

## Challenge Description

> Run the Python script and convert the given number from decimal to binary to get the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the directory to locate the target script:

```
ls -la
```

The directory contains `convertme.py`. Reading the script reveals that it selects a random integer, asks the user to convert it to base 2, and prints the decrypted flag upon receiving the correct input.

### 2. Execution & Binary Conversion

Run the script using Python 3:

```
python3 convertme.py
```

The script asks a question in the following format:

```text
If 43 is in decimal (base 10), what is it in binary (base 2)?
Answer: 
```

To compute the binary representation directly in another terminal or shell session:

```
python3 -c "print(bin(43)[2:])"
```

Or using `bc`:

```
echo "obase=2; 43" | bc
```

Both methods yield `101011`.

### 3. Execution & Flag Capture

Provide the calculated binary string to the active prompt:

```text
Answer: 101011
That is correct! Here is your flag: academy{4ll_y0ur_b4535_........}
```

The full flag is printed:

```
academy{4ll_y0ur_b4535_........}
```

## Remediation & Key Takeaways

* **Positional Radix Conversion:** Base 10 numbers are converted to Base 2 by recording remainders of successive divisions by 2 or summing active bit weights ($2^0, 2^1, 2^2, \dots$).
* **CLI Quick Calculations:** One-line commands such as `python3 -c "print(bin(<num>)[2:])"` or `bc` provide instant conversions without using web-based calculators.
* **Static Inspection:** Python source code can be inspected directly to review validation routines or extract obfuscated strings if interactive execution is constrained.
