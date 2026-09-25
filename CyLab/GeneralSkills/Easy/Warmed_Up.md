# picoCTF – Warmed Up Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Warmed Up
* **Category:** General Skills
* **Points:** 50
* **Date:** 9/25/2026
* **Flag:** academy{..}

---

## TL;DR (Abstract)
The challenge provides a hexadecimal number (`0x3D`) and asks for its decimal equivalent. Converting the hex value directly to base-10 yields `61`, which when placed in the flag format completes the challenge.

---

## Challenge Description
> What is 0x3D (base 16) in decimal (base 10)? Submit your answer in our flag format. For example, if your answer was '22', you would submit 'academy{22}'.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
The challenge requires converting a hexadecimal (base 16) literal into standard decimal (base 10):
* Input: `0x3D`
* Base: 16 -> 10

### 2. Base Conversion Calculation
In hexadecimal:
* The digit `3` is in the 16s place ($16^1 = 16$).
* The digit `D` represents 13 in decimal and is in the 1s place ($16^0 = 1$).

Calculating manually:
$$(3 \times 16^1) + (13 \times 16^0) = 48 + 13 = 61$$

You can also compute this directly in the terminal using Bash arithmetic expansion:

```bash
echo $((0x3D))
```

Or using Python:

```bash
python3 -c "print(int('0x3D', 16))"
```

Both commands output:
```text
61
```

### 3. Flag Capture
Format the calculated decimal value into the required flag wrapper:

```text
academy{..}
```

---

## Remediation & Key Takeaways
* **Hexadecimal Basics:** Hex uses base-16 with characters 0-9 and A-F (A=10 through F=15).
* **Positional Weight:** Each place value represents an increasing power of 16 starting from $16^0$ on the far right.
* **Shell Arithmetic:** Modern shells (bash, zsh) evaluate hex prefixes (`0x`) directly inside `$((...))` arithmetic expressions.
