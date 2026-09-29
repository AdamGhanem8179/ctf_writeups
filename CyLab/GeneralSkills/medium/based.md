# CyLab – based Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** based

* **Category:** General Skills / Cryptography

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{learning_about_converting_values_........}

## TL;DR (Abstract)

The challenge exposes an interactive network service over Netcat that prompts the user to convert values across multiple numeral systems (binary, octal, hexadecimal) into their plaintext ASCII representations under a strict countdown timer. By parsing each presented base and rapidly decoding the character values in real time, all consecutive stages were completed to retrieve the flag.

## Challenge Description

> To get truly "based", you'll need to know your conversion tables. Connect over netcat to convert values in real time before the timer expires.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connect to the provided challenge service using Netcat:

```bash
nc <host> <port>
```

The challenge operates in a dynamic prompt-and-response format with a countdown (typically 45 seconds per round). Each stage requires converting a string encoded in a specific number base back to standard ASCII:

1. **Stage 1 (Binary):** A sequence of 8-bit binary strings (e.g., `01110100 01100101 01110011 01110100`).
2. **Stage 2 (Octal):** A sequence of octal values (base-8 numbers).
3. **Stage 3 (Hexadecimal):** A packed or spaced hex string (base-16 representation).

### 2. Live Conversion Strategy

Because of the time limit, conversions were calculated quickly using a local terminal session or Python interpreter.

#### Stage 1: Binary to ASCII
Given binary bytes separated by spaces:
```python
binary_str = "01110100 01100101 01110011 01110100"  # example prompt
word = "".join(chr(int(b, 2)) for b in binary_str.split())
print(word)
```

#### Stage 2: Octal to ASCII
Given octal values:
```python
octal_str = "164 145 163 164"  # example prompt
word = "".join(chr(int(o, 8)) for o in octal_str.split())
print(word)
```

#### Stage 3: Hexadecimal to ASCII
Given a hex string:
```python
hex_str = "74657374"  # example prompt
word = bytes.fromhex(hex_str).decode("utf-8")
print(word)
```

### 3. Execution & Flag Capture

Submitting the decoded words within the allotted time satisfied all challenge stages. Upon successful completion of the final stage, the server returned the flag:

```text
academy{learning_about_converting_values_........}
```

Flag:

```text
academy{learning_about_converting_values_........}
```
