# picoCTF – binhexa Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** binhexa

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{b1tw^3se_0p3eR@tI0n_su33essFuL_........}

## TL;DR (Abstract)

The challenge connects over `nc` (netcat) to a dynamic binary math quiz that tests basic bitwise operations (`AND`, `OR`, `XOR`, left shift `<<`, right shift `>>`) and base arithmetic on binary numbers. By solving each prompt in sequence and submitting the final result in hexadecimal format as requested by the server, the remote service verifies the calculations and outputs the flag.

## Challenge Description

> How well can you check the bits?
> Connect to the program with `nc <host> <port>` to solve the binary calculations.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connecting to the challenge server via netcat prompts an interactive terminal session:

```bash
nc <host> <port>
```

The service generates two random binary numbers (e.g., `Binary Number 1: 01011010`, `Binary Number 2: 00111100`) and presents a sequence of operations to perform:

1. **Bitwise AND (`&`):** Output `1` only if both corresponding bits are `1`.
2. **Bitwise OR (`|`):** Output `1` if at least one corresponding bit is `1`.
3. **Bitwise XOR (`^`):** Output `1` if bits differ, `0` if they are identical.
4. **Left / Right Shift (`<<`, `>>`):** Shift the bit pattern by $n$ positions, padding with zeros.
5. **Addition (`+`):** Perform standard binary addition with carries.

### 2. Solving Operations via CLI

Rather than performing multi-step manual binary arithmetic under potential timeout limits, Python provides immediate evaluation directly from a second terminal window.

Example interactive workflow using `python3`:

```python
# Convert binary literals directly using 0b prefix
n1 = 0b01011010
n2 = 0b00111100

# Bitwise AND:
print(bin(n1 & n2)[2:])

# Bitwise OR:
print(bin(n1 | n2)[2:])

# Bitwise XOR:
print(bin(n1 ^ n2)[2:])

# Left shift Number 1 by 1:
print(bin(n1 << 1)[2:])

# Right shift Number 2 by 1:
print(bin(n2 >> 1)[2:])
```

For the final prompt, the server requests the answer to be submitted in **Hexadecimal (base 16)**:

```python
# Convert the final calculation to Hexadecimal
result = n1 + n2
print(hex(result)[2:].upper())
```

### 3. Execution & Flag Capture

Entering each answer into the netcat prompt verifies all stages:

```text
Welcome to the Binary-Hex Quiz!
...
Operation 1: Enter the binary result of (Number 1 & Number 2)
> 00011000
Correct!

Operation 2: Enter the binary result of (Number 1 | Number 2)
> 01111110
Correct!

Operation 3: Enter the binary result of (Number 1 ^ Number 2)
> 01100110
Correct!

...

Final Question: Enter the results in Hexadecimal:
> 96
Correct!

You have completed all questions!
Here is your flag: academy{b1tw^3se_0p3eR@tI0n_su33essFuL_........}
```

The service completes verification and outputs the flag:

```text
academy{b1tw^3se_0p3eR@tI0n_su33essFuL_........}
```

## Remediation & Key Takeaways

* **Truth Tables:** 
  * `AND (&)`: True only when $A = 1$ and $B = 1$.
  * `OR (|)`: True when either $A = 1$ or $B = 1$.
  * `XOR (^)`: True strictly when $A \neq B$.
* **Bit Shifts:** Shifting left (`<< 1`) multiplies the integer by 2, while shifting right (`>> 1`) performs floor division by 2.
* **Radix Translation:** Python's built-in `bin()`, `hex()`, and `int(string, base)` functions allow rapid manipulation and verification of multi-radix values during real-time CTF challenges.
