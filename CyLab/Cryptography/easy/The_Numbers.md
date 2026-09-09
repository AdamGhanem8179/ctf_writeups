# picoCTF 2026 – The Numbers Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** The Numbers
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `PICOCTF{THENUMB........}`

---

## TL;DR (Abstract)
The challenge presents an image containing a sequence of space-separated integers punctuated by curly braces (`{ }`). Recognizing that the curly braces matched standard CTF flag syntax, the initial integer count before the opening brace was checked against the length of the string `PICOCTF` (7 characters). The lengths aligned perfectly, confirming an A1Z26 substitution cipher ($1 = A, 2 = B, \dots, 26 = Z$). Mapping each integer to its corresponding alphabetical position directly recovered the full plaintext flag.

---

## Challenge Description
> The numbers... what do they mean?
> 
> Download the image file provided in the challenge: `the_numbers.png`

---

## Thought Process & Walkthrough

### 1. Visual Inspection & Format Recognition
Opening the provided image displays a sequence of integers:

```text
16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }
```

The presence of literal `{` and `}` characters immediately indicates the flag wrapper structure. 

Counting the numbers before the opening brace gives 7 integers:
```text
16  9  3  15  3  20  6
```

Comparing this against the expected flag prefix `PICOCTF`:
* Length of `PICOCTF` = 7 characters
* Number count before `{` = 7

### 2. Validating the Cipher (A1Z26)
Testing the hypothesis that each number represents its 1-indexed alphabetical position ($A=1, B=2, \dots, Z=26$):

* $16 \rightarrow \text{P}$
* $9 \rightarrow \text{I}$
* $3 \rightarrow \text{C}$
* $15 \rightarrow \text{O}$
* $3 \rightarrow \text{C}$
* $20 \rightarrow \text{T}$
* $6 \rightarrow \text{F}$

The prefix resolves to `PICOCTF`, verifying the mapping.

### 3. Decoding the Flag Payload
Apply the same $N \rightarrow \text{char}(64 + N)$ translation to the numbers inside the brackets:

* $20 \rightarrow \text{T}$
* $8 \rightarrow \text{H}$
* $5 \rightarrow \text{E}$
* $14 \rightarrow \text{N}$
* $21 \rightarrow \text{U}$
* $13 \rightarrow \text{M}$
* $2 \rightarrow \text{B}$
* $5 \rightarrow \text{E}$
* $18 \rightarrow \text{R}$
* $19 \rightarrow \text{S}$
* $13 \rightarrow \text{M}$
* $1 \rightarrow \text{A}$
* $19 \rightarrow \text{S}$
* $15 \rightarrow \text{O}$
* $14 \rightarrow \text{N}$

Concatenating the translated letters produces:
```text
THENUMBERSMASON
```

Wrapping with the verified prefix and braces gives the final flag:

```text
PICOCTF{THENUMB........}
```

Alternatively, this can be solved instantly with a one-line Python command:
```python
nums = "20 8 5 14 21 13 2 5 18 19 13 1 19 15 14".split()
print("PICOCTF{" + "".join(chr(int(n) + 64) for n in nums) + "}")
```

---

## Remediation & Key Takeaways
* **A1Z26 is Encoding, Not Encryption:** Simple numeric-to-alphabet substitutions do not provide security and can be broken instantly by frequency analysis or known-plaintext prefix matching (such as CTF flag wrappers).
* **Pattern Leakage:** Maintaining structural formatting (like `{}`) while encoding surrounding text exposes the underlying grammar and significantly accelerates cryptanalysis.
