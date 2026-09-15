# CyLab 2026 – Bytemancy 1 Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Bytemancy 1
* **Category:** Reverse Engineering / Binary Exploitation
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{h0w_m4ny_e's???_0c1ad83a}

---

## TL;DR (Abstract)
The challenge provides an interactive binary that prompts for a specific input sequence to validate internal control flow. Following the pattern of byte evaluation, the routine counts or matches occurrences of the letter 'e' (ASCII `0x65`). Supplying the expected count or string sequence satisfies the conditional jump, steering execution into the flag disclosure function and printing the flag to the terminal.

---

## Challenge Description
> The arcane terminal returns with a sequel. How many e's does it take to appease the byte wizards this time? Provide the correct sequence and reveal the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Connect to the challenge server or execute the binary locally:

./bytemancy1

The program requests user input at the interactive prompt:

Enter spell/bytes: 

### 2. Evaluating Input Requirements
The challenge hints at determining the exact number or sequence of the character `e`. Supplying the target sequence of `e` characters satisfies the binary's internal comparison loop or length/byte count check.

### 3. Triggering the Win Condition & Flag Capture
Once the input matches the expected byte criteria, the application bypasses the failure routine and executes the win handler, printing the flag directly to stdout:

picoCTF{h0w_m4ny_e's???_0c1ad83a}

---

## Remediation & Key Takeaways
* **Avoid Predictable Input Checks:** Relying on simple character-count loops or recurring ASCII checks allows players to easily guess or brute-force valid inputs.
* **Use Robust Key Derivation:** Instead of branching to an unencrypted flag-printing routine based on a plaintext check, derive the decryption key directly from a strong, hashed passkey.
* **Strip Informative Metadata:** Challenge flags should not be stored in cleartext inside binary memory or loaded via straightforward win functions without server-side validation.
