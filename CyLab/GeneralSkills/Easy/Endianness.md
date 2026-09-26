# CyLab – Endianness Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Endianness

* **Category:** General Skills / Binary Exploitation

* **Points:** 50

* **Date:** 9/26/2026

* **Flag:** academy{3ndi4n_sw4p_su33ess\_........}

## TL;DR (Abstract)

The challenge tests understanding of byte order representations: Little Endian and Big Endian. Given a target word, the user is required to calculate and submit both the Little Endian and Big Endian hexadecimal byte representations. Supplying both valid representations outputs the flag.

## Challenge Description

> Connect to the service, convert the provided word into both Little Endian and Big Endian hexadecimal representations, and claim the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Endianness defines how multi-byte data types are ordered in computer memory:

* **Big Endian:** The most significant byte (MSB) is stored at the lowest memory address (natural left-to-right byte order).
* **Little Endian:** The least significant byte (LSB) is stored at the lowest memory address (bytes are reversed).

### 2. Byte Order Conversion

Given an input string:

1. Determine the hexadecimal ASCII byte values for each character.
2. **Big Endian:** Preserves the natural byte order of the ASCII hex values.
3. **Little Endian:** Inverts the sequence of bytes from end to beginning.

### 3. Execution & Flag Capture

Connect to the challenge service via `nc`:

```bash
nc <challenge-host> <port>
```

Submit the Little Endian and Big Endian hex strings when prompted by the interactive shell:

```text
Enter the Little Endian representation: <little_endian_hex>
Enter the Big Endian representation: <big_endian_hex>
```

Terminal Output:

```text
academy{3ndi4n_sw4p_su33ess_........}
```

Flag:

```
academy{3ndi4n_sw4p_su33ess_........}
```
