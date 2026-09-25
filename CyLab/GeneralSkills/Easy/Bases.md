# picoCTF – Bases Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Bases

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{l3arn_th3_.....}

## TL;DR (Abstract)

The challenge presents a ciphertext encoded in Base64 (`bDNhcm5fdGgzX3IwcDM1`). By piping the encoded string directly into the Linux utility `base64 -d`, the payload was decoded into plain text (`l3arn_th3_r0p35`) and placed inside the flag wrapper.

## Challenge Description

> What does this `bDNhcm5fdGgzX3IwcDM1` mean? I think it has something to do with bases.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge prompt provides an encoded string:

```
bDNhcm5fdGgzX3IwcDM1
```

Characteristics of the string:
* Consists of alphanumeric ASCII characters (uppercase, lowercase, numbers).
* Fits standard Base64 character sets and length conventions.

### 2. Decoding with Base64

Base64 is a binary-to-text encoding scheme that represents binary data in an ASCII string format by translating it into a radix-64 representation. In standard Unix/Linux environments, the `base64` utility handles decoding using the `-d` (or `--decode`) flag.

### 3. Execution & Flag Capture

Pipe the string into `base64 -d`:

```
echo 'bDNhcm5fdGgzX3IwcDM1' | base64 -d
```

Terminal Output:

```
l3arn_th3_.....
```

Wrapping the decoded output in the challenge format yields the final flag:

```
academy{l3arn_th3_.....}
```

## Remediation & Key Takeaways

* **Base64 Characteristics:** Base64 strings consist of `A-Z`, `a-z`, `0-9`, `+`, `/`, and often use `=` for padding at the end.
* **CLI Stream Decoding:** Using `echo '<string>' | base64 -d` provides immediate command-line decoding without needing third-party online converters.
* **Encoding vs. Encryption:** Base64 is an encoding mechanism designed for safe data transport across text protocols, not encryption; it provides no confidentiality or data security.
