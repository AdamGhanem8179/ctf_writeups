# CyLab 2026 – Bytemancy Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Bytemancy
* **Category:** Reverse Engineering / Binary Exploitation
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{pr1n74813_ch4r5_15ddc7a7}

---

## TL;DR (Abstract)
The challenge provides an interactive binary that prompts the user for string input, evaluating it against specific byte values, character codes, or an offset check to trigger the victory condition. Providing the character sequence `eee` satisfied the internal validation check (likely matching target ASCII byte representations such as `0x65`), triggering the function that prints the flag directly to the terminal.

---

## Challenge Description
> Master the magic of bytes! Interact with the arcane terminal prompt, satisfy the program's input spell, and extract the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Connect to the challenge instance or execute the provided binary:

./bytemancy

The binary prompts the user with an interactive terminal interface requesting input:

Enter spell/bytes: 

### 2. Testing Input & Byte Evaluation
The program evaluates user-supplied input against internal character or byte conditions. When providing the input string `eee`:

eee

The program parses the ASCII character values (`0x65 0x65 0x65`). This input satisfies the targeted branching condition or comparison register in the binary logic.

### 3. Triggering Win Condition & Flag Capture
Upon matching the expected byte pattern, execution branches directly to the routine that unlocks and outputs the flag:

Spell accepted!
picoCTF{pr1n74813_ch4r5_15ddc7a7}

---

## Remediation & Key Takeaways
* **Avoid Hardcoded or Trivial Check Logic:** Simple multi-byte checks (such as checking matching characters like `eee`) can be easily bypassed through trivial fuzzing or brute-force input without needing in-depth reverse engineering.
* **Enforce Strong Cryptographic Verification:** Key-verification logic should rely on one-way hashing or cryptographic signatures rather than static string or character-by-character checks.
* **Disable Plaintext Win Functions:** Avoid compiling binaries with unconditioned flag-printing routines directly accessible via basic control-flow branches.
