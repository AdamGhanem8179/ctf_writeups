# CyLab 2026 – Multicode Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Multicode
* **Category:** Cryptography
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{nested_enc0ding_82499dad}

---

## TL;DR (Abstract)
The challenge provides an encoded ciphertext string that has been obfuscated through multiple layers of standard encoding schemes and ciphers. By identifying each layer sequentially and unwrapping them in reverse order—decoding Base64, converting Hexadecimal to ASCII, decoding URL percent-encoding, and finally applying a ROT/Caesar rotation—the plaintext payload is recovered, revealing the flag.

---

## Challenge Description
> Can you unravel the layered protections hiding this secret? Trace through the nested encoding schemes step-by-step to recover the original message.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Inspect the provided encoded text file or output string:

cat encoded.txt

The outermost string exhibits standard Base64 characteristics (alphanumeric characters, typical padding with =).

### 2. Sequential Decoding Pipeline
Unwrap each layer step-by-step using terminal utilities or CyberChef:

1. Base64 Decoding:
   Decode the raw payload from Base64:
   cat encoded.txt | base64 -d
   The result yields a stream of hexadecimal bytes (e.g., pairs of 0-9 and a-f).

2. Hexadecimal to ASCII:
   Convert the hex string into readable ASCII text:
   echo "<hex_string>" | xxd -r -p
   The output exposes URL percent-encoded characters (e.g., %20, %7B, %7D).

3. URL Decoding:
   Decode the percent-encoded string:
   python3 -c "import urllib.parse, sys; print(urllib.parse.unquote(sys.stdin.read()))"
   The resulting text resembles flag formatting but with shifted alphabetic characters.

4. ROT / Caesar Cipher:
   Rotate the alphabet to correct the Caesar shift (ROT13 or target shift offset) to align with the standard picoCTF{...} prefix.

### 3. Flag Capture
Executing the complete unwrapping pipeline yields the plaintext flag:

picoCTF{nested_enc0ding_82499dad}

---

## Remediation & Key Takeaways
* **Encoding is Not Encryption:** Layering multiple standard encoding formats (Base64, Hex, URL) provides zero confidentiality; each layer is deterministic, unkeyed, and trivially reversible.
* **Avoid Security Through Obscurity:** Chaining simple substitutions and encodings cannot replace modern, keyed cryptographic standards such as AES-GCM or ChaCha20-Poly1305.
* **Identify Data Signatures:** Recognizing distinct data representations (Base64 padding, hex byte pairs, percent-encoded URL markers) allows rapid identification and automation of decoding pipelines.
