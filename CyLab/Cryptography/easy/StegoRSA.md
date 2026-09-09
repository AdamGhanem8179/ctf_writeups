# picoCTF 2026 – StegoRSA Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** StegoRSA
* **Category:** Cryptography / Steganography
* **Points:** 100
* **Date:** 9/9/2026
* **Flag:** `picoCTF{rs4_k3y_1n_1mg_........}`

---

## TL;DR (Abstract)
The challenge combines basic image metadata steganography with RSA public-key decryption. Inspecting the provided JPEG image with the file utility revealed a hidden hex-encoded string stored inside the JFIF comment field rather than within modified pixel data. Extracting and hex-decoding the complete `0xFFFE` (COM) marker segment recovered an intact PEM-formatted RSA private key. Passing the private key and the encrypted payload into OpenSSL immediately decrypted the ciphertext to yield the flag.

---

## Challenge Description
> Can you recover the secret message hidden within this image?
> 
> Files provided: `image.jpg`, `flag.enc`

---

## Thought Process & Walkthrough

### 1. Metadata Inspection Over Pixel Stego
Rather than jumping straight to complex LSB or frequency-domain steganography tools, standard initial recon on `image.jpg` was performed using the `file` command:

```bash
file image.jpg
```

The output revealed a non-standard JPEG comment field (`comment: ...`) containing long sequences of hexadecimal characters. This confirmed that the challenge relied on simple metadata concealment instead of pixel-based steganographic encoding.

### 2. Extracting the JPEG Comment Segment
Because command-line file previews often truncate long metadata fields, the full `0xFFFE` (COM) marker segment was extracted cleanly from the file headers.

Using `exiftool` or `strings` to dump the raw comment payload:
```bash
exiftool -Comment -b image.jpg > comment_hex.txt
```

Hex-decoding the extracted string:
```bash
xxd -r -p comment_hex.txt > private_key.pem
```

Inspecting `private_key.pem` confirmed a valid, complete RSA private key header:
```text
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA...
...
-----END RSA PRIVATE KEY-----
```

### 3. Decrypting the Flag
With the RSA private key recovered, decrypting `flag.enc` was completed using OpenSSL's `pkeyutl` utility:

```bash
openssl pkeyutl -decrypt -inkey private_key.pem -in flag.enc
```

The command processed the ciphertext and printed the flag:

```text
picoCTF{rs4_k3y_1n_1mg_........}
```

---

## Remediation & Key Takeaways
* **Scrub Metadata in Public Assets:** Image comment fields (`COM` marker segments) and EXIF blocks are plaintext metadata easily read by standard file inspection tools. Strip all metadata using tools like `exiftool -all= image.jpg` before distributing files.
* **Never Embed Private Keys in Unencrypted Assets:** Private keys must never be packaged inside public binaries or media files. Keep cryptographic keys stored securely in hardware security modules (HSM) or encrypted key vaults with strict access controls.
