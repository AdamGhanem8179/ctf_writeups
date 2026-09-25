# picoCTF – strings it Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** strings it

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{5tRIng5_1T_........}

## TL;DR (Abstract)

The challenge provides an unstripped binary containing massive amounts of garbage data and printable strings. By passing the binary to the `strings` utility and filtering the standard output through an extended regular expression with `grep` (`strings strings | grep -oE '[A-Za-z0-9_]+\{[^}]*\}'`), the embedded flag was instantly extracted.

## Challenge Description

> Can you find the flag in file without running it?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the target file `strings`. Running `file strings` indicates it is an executable binary. Since the goal is to locate the flag without execution, inspecting human-readable strings embedded in the binary is the primary approach.

### 2. Stream Extraction & Regex Filtering

Direct inspection of `strings strings` produces thousands of lines. To extract only the flag format, the stream is filtered directly with `grep` using an extended regular expression:

* `strings strings`: Extracts all consecutive printable character sequences from the binary.

* `grep -oE '[A-Za-z0-9_]+\{[^}]*\}'`:
  * `-E`: Enables extended regular expressions.
  * `-o`: Prints only the matching segment rather than the entire line.
  * `[A-Za-z0-9_]+`: Matches the flag prefix.
  * `\{[^}]*\}`: Matches the opening brace, characters inside, and closing brace.

### 3. Executing the Command & Flag Capture

Run the pipeline:

```
strings strings | grep -oE '[A-Za-z0-9_]+\{[^}]*\}'

```

Terminal Output:

```
academy{5tRIng5_1T_........}

```

## Remediation & Key Takeaways

* **Static Binary Inspection:** The `strings` utility extracts ASCII and printable UTF-8 sequences from binaries, often exposing hardcoded secrets, debug messages, and flags without executing untrusted code.

* **Precise Pattern Matching:** Using `grep -oE` with regex patterns targeting `prefix{...}` isolates flags from noisy binary dumps efficiently.

* **Stream Piping:** Chaining Unix CLI utilities avoids saving intermediate files and simplifies terminal workflows during CTF reconnaissance.
