# picoCTF – 2Warm Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** 2Warm

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/25/2026

* **Flag:** academy{......}

## TL;DR (Abstract)

The challenge asks to convert the decimal number `42` into binary (base 2). By performing successive division by 2 or using standard command-line tools like Python or `bc`, the value was converted to `101010` and placed inside the flag wrapper.

## Challenge Description

> Can you convert the number 42 (base 10) to binary (base 2)?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge provides a direct numerical conversion task:
* Input: `42` in base 10 (decimal).
* Target: base 2 (binary).

### 2. Manual Conversion via Successive Division

To convert a decimal number to binary manually, repeatedly divide the quotient by 2 and record the remainders from least significant bit (LSB) to most significant bit (MSB):

* $42 \div 2 = 21$ remainder **0** (LSB)
* $21 \div 2 = 10$ remainder **1**
* $10 \div 2 = 5$ remainder **0**
* $5 \div 2 = 2$ remainder **1**
* $2 \div 2 = 1$ remainder **0**
* $1 \div 2 = 0$ remainder **1** (MSB)

Reading the remainders from bottom to top yields:

```
101010
```

### 3. Execution & Flag Capture

The conversion can also be performed via the terminal using Python:

```bash
python3 -c "print(bin(42)[2:])"
```

Or using the standard Unix `bc` (Basic Calculator) utility:

```bash
echo "obase=2; 42" | bc
```

Terminal Output:

```
......
```

Wrapping the decoded output in the challenge format yields the final flag:

```
academy{......}
```

## Remediation & Key Takeaways

* **Radix Representations:** Base 10 uses digits `0-9`, while Base 2 (binary) relies exclusively on `0` and `1` to represent powers of 2.
* **CLI Conversions:** Built-in Linux tools such as `python3` (`bin()`, `hex()`, `oct()`) and `bc` (`obase`, `ibase`) provide fast, scriptable base conversions directly from the terminal without external tools.
* **Positional Notation:** $101010_2 = (1 \times 2^5) + (0 \times 2^4) + (1 \times 2^3) + (0 \times 2^2) + (1 \times 2^1) + (0 \times 2^0) = 32 + 8 + 2 = 42_{10}$.
