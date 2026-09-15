# CyLab 2026 – Piece by Piece Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Piece by Piece
* **Category:** Forensics / General Skills
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_........}

---

## TL;DR (Abstract)
The challenge provides a password-protected ZIP archive that has been split into multiple fragment files (`part_a*`) using standard Unix splitting utilities. By using `cat` to concatenate all split chunks in alphabetical order into a single unified archive file (`combined.zip`), the original ZIP container is reconstructed. Supplying the known or discovered password (`supersecret`) to `unzip` decompresses the archive and extracts `flag.txt`, revealing the challenge flag.

---

## Challenge Description
> The secret was broken into pieces and locked inside an archive. Reassemble the fragments, unlock the container, and extract the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Inspect the challenge environment and examine the available files:

ls -la

The directory contains multiple file chunks split from an archive (e.g., `part_aa`, `part_ab`, etc.) alongside an identified password requirement.

### 2. Recombining the Archive Fragments
Concatenate all partial fragments in sequential order back into a single archive file:

cat part_a* > combined.zip

### 3. Extracting the Protected Archive
Unzip the newly assembled `combined.zip` archive by passing the password `supersecret`:

unzip -P supersecret combined.zip

Terminal output confirms successful decompression:

Archive:  combined.zip
 extracting: flag.txt

### 4. Reading the Flag
Inspect the contents of the extracted `flag.txt` file:

cat flag.txt

The shell outputs the full flag:

picoCTF{z1p_and_spl1t_f1l3s_4r3_fun_........}

---

## Remediation & Key Takeaways
* **Reconstructing Segmented Data:** Standard split files created via utilities like `split` retain sequential byte boundaries, allowing trivial byte-level reconstruction using simple binary concatenation via `cat`.
* **Weakness of Legacy ZIP Encryption:** Standard ZIP encryption (ZipCrypto) is mathematically weak and prone to known-plaintext attacks; password-protected archives should employ modern encryption standards such as AES-256 (e.g., via 7z or GPG).
* **Hardcoded / Shared Passwords:** Avoid using weak or easily discoverable passwords like `supersecret` for sensitive archives, as they provide negligible defense against unauthorized extraction.
