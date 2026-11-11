# Natas Level 8 Write-up

## Step 0 - Challenge Info

* **CTF Name:** OverTheWire Natas

* **Challenge Name:** Level 8 to Level 9

* **Category:** Web Exploitation / Reverse Engineering

* **Difficulty:** Beginner

* **Date:** 2026-11-11

* **Flag:** `UdxmI27dTaXmnd1rxKQTfws6........`

## TL;DR (Abstract)

The web application's source code exposed an encoded secret string alongside the exact PHP function used to encode it. By reversing the encoding steps in the terminal using `xxd`, `rev`, and `base64`, the original secret was recovered and submitted to retrieve the flag.

## Challenge Description

> The challenge presents a form asking for a secret to reveal the password for the next level. Inspecting the provided source code reveals both the encoded target string and the custom algorithm used to obscure it.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

Viewing the PHP source code exposed a custom encoding function and an encoded secret:

```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

The application checks if the user's input, when passed through `encodeSecret()`, matches `$encodedSecret`.

### 2. Reverse Engineering the Algorithm

Because the exact encoding algorithm was left in the source code, it could be perfectly reversed. The original function processes the string in three steps:
1. `base64_encode`
2. `strrev` (string reverse)
3. `bin2hex` (binary to hexadecimal)

To find the plaintext secret, I needed to perform the exact opposite operations in reverse order:
1. Hexadecimal to binary/ASCII
2. String reverse
3. Base64 decode

### 3. Execution & Flag Capture

I used a chain of Linux command-line tools to reverse the operations on the encoded string:

```bash
echo "3d3d516343746d4d6d6c315669563362" | xxd -r -p | rev | base64 -d
```

* `xxd -r -p` reversed the `bin2hex` operation.
* `rev` reversed the `strrev` operation.
* `base64 -d` reversed the `base64_encode` operation.

This command output the decoded plaintext secret. Submitting this secret into the web form successfully authenticated the session and revealed the password for the next level:

```
Access granted. The password for natas9 is UdxmI27dTaXmnd1rxKQTfws6........
```

## Mitigation & Lessons Learned

* **Defense:** Do not use reversible encoding (like Base64 or Hex) as a substitute for encryption or hashing. If a secret must be verified, store a strong cryptographic hash (e.g., bcrypt or Argon2) of the secret on the backend, rather than the plaintext or encoded version. 

* **Takeaway:** "Security through obscurity" is not effective. Leaving the blueprint for how data is obfuscated (the encoding steps) right next to the obfuscated data makes reverse engineering trivial. Never expose cryptographic or encoding logic and secrets to the client side.
