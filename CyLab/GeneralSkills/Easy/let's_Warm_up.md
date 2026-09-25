# picoCTF – Lets Warm Up Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Lets Warm Up

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/25/2026

* **Flag:** academy{.}

## TL;DR (Abstract)

The challenge presents a hexadecimal byte value (`0x70`) and asks to decode it into its corresponding ASCII character. Converting the hex code $0x70$ (decimal 112) into standard ASCII yields the lowercase character `p`, producing the flag `academy{p}`.

## Challenge Description

> If I told you a word started with 0x70 in hexadecimal, what would it start with in ASCII? Submit your answer in our flag format.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge asks to decode a single hexadecimal byte into its ASCII character representation:

* Input byte: `0x70`

* Target format: ASCII character wrapped inside `academy{...}`

### 2. Hex to ASCII Decoding

In hexadecimal, each byte corresponds to an ASCII code point:

* Hexadecimal `0x70` converts to decimal:

$$
(7 \times 16^1) + (0 \times 16^0) = 112
$$

* In standard ASCII tables, the decimal value $112$ maps to the lowercase character `p`.

This can be verified instantly in the terminal:

Using `printf`:

```
printf "\x70\n"

```

Using Python:

```
python3 -c "print(chr(0x70))"

```

Both commands output:

```
p

```

### 3. Flag Capture

Wrapping the recovered character into the challenge flag wrapper gives:

```
academy{.}

```

## Remediation & Key Takeaways

* **ASCII Table Mapping:** Standard ASCII characters reside between hex values `0x00` and `0x7F`. Printable characters range from `0x20` (space) to `0x7E` (`~`).

* **Quick Shell Decoding:** The shell utility `printf "\xHH"` renders any arbitrary hexadecimal byte `HH` directly as its raw ASCII equivalent.

* **Binary Representation:** Hexadecimal is widely used in CTFs and reverse engineering because two hex digits neatly represent one complete 8-bit byte ($2^8 = 256$ states).
