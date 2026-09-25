# picoCTF – repetitions Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** repetitions

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{base64_n3st3d_dic0d!n8_d0wnl04d3d_........}

## TL;DR (Abstract)

The challenge provides a file containing a payload that has been repeatedly encoded using Base64. By iteratively piping the output back into the `base64 -d` decoding utility—either manually through chained CLI pipes or via a brief loop—the multiple encoding layers are stripped away to reveal the plaintext flag.

## Challenge Description

> Can you make sense of this file?
> Download the file `enc_flag`.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the file contents and type using standard Unix utilities:

```bash
file enc_flag
cat enc_flag
```

The file contains a single continuous ASCII string consisting of alphanumeric characters, `+`, `/`, and `=` padding indicators—the standard character set of Base64 encoding.

### 2. Multi-Layer Decoding Analysis

A single Base64 decode operation reveals that the payload does not decode directly into standard text; instead, it outputs another layer of Base64-encoded ciphertext:

```bash
cat enc_flag | base64 -d
```

Because the challenge title is **repetitions**, the string is nested through multiple cycles of Base64 encoding.

### 3. Execution & Flag Capture

#### Method A: Chained Pipeline

The layers can be peeled back in the shell by piping multiple `base64 -d` commands sequentially until the flag format appears:

```bash
cat enc_flag | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d | base64 -d
```

#### Method B: Automated Bash While-Loop

Alternatively, an iterative bash loop decodes the payload until the flag wrapper pattern (`academy{` or `picoCTF{`) is identified:

```bash
cp enc_flag temp.txt
while ! grep -q "academy{" temp.txt; do
    base64 -d temp.txt > next.txt 2>/dev/null && mv next.txt temp.txt
done
cat temp.txt
```

#### Method C: Python Iteration

```python
import base64

with open("enc_flag", "r") as f:
    data = f.read().strip()

while True:
    try:
        data = base64.b64decode(data).decode('utf-8')
        if "academy{" in data:
            print("Flag found:", data)
            break
    except Exception:
        break
```

Terminal Output:

```text
academy{base64_n3st3d_dic0d!n8_d0wnl04d3d_........}
```

The nested encoding resolves to the final flag:

```
academy{base64_n3st3d_dic0d!n8_d0wnl04d3d_........}
```

## Remediation & Key Takeaways

* **Base64 Is Encoding, Not Encryption:** Base64 is a binary-to-text representation scheme, not an encryption algorithm. Repeating the transformation adds computational steps but zero cryptographic security.
* **CLI Stream Pipelining:** Unix pipes (`|`) make multi-pass decoding trivial directly in the terminal without writing helper files to disk.
* **Padding Signatures:** The trailing `=` or `==` characters indicate the byte-alignment padding typical of Base64 representations.
