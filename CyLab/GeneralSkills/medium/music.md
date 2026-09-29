# CyLab – mus1c Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** mus1c

* **Category:** General Skills / Esoteric Languages

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{rrrocknrn0113r}

## TL;DR (Abstract)

The challenge provides a text file containing song lyrics that actually represent valid source code written in the esoteric programming language **Rockstar**. By executing the code inside the online Rockstar interpreter (`codewithrockstar.com`), the program outputs a sequence of decimal numbers. Converting these decimal values into their corresponding ASCII characters reconstructs the plaintext flag.

## Challenge Description

> I wrote you a song. Put it in the flag format: `academy{...}`

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the provided file (e.g., `lyrics.txt`):

* **Content:** Looks like poetic rock-and-roll song lyrics, containing lines with keywords like `Put`, `Listen`, `Shout`, and `Scream`.
* **Identification:** The syntax corresponds to **Rockstar**, an esoteric programming language designed for code to resemble 1980s power ballad lyrics.

### 2. Executing Rockstar Code

1. Navigate to the online Rockstar interpreter: [codewithrockstar.com/online](https://codewithrockstar.com/online).
2. Paste the provided song lyrics into the input editor and run the code.
3. The program executes and outputs the following sequence of decimal numbers:

```text
114
114
114
111
99
107
110
114
110
48
49
49
51
114
```

### 3. ASCII Decoding

Each number corresponds to a decimal ASCII character code:

| Decimal | ASCII Character |
| :--- | :--- |
| `114` | `r` |
| `114` | `r` |
| `114` | `r` |
| `111` | `o` |
| `99`  | `c` |
| `107` | `k` |
| `110` | `n` |
| `114` | `r` |
| `110` | `n` |
| `48`  | `0` |
| `49`  | `1` |
| `49`  | `1` |
| `51`  | `3` |
| `114` | `r` |

Using a quick Python one-liner to parse the numbers:

```bash
python3 -c '
nums = [114, 114, 114, 111, 99, 107, 110, 114, 110, 48, 49, 49, 51, 114]
print("".join(chr(c) for c in nums))
'
```

Output:
```text
rrrocknrn0113r
```

### 4. Execution & Flag Capture

Wrapping the decoded string into the standard format yields the final flag:

```text
academy{rrrocknrn0113r}
```

Flag:

```text
academy{rrrocknrn0113r}
```
