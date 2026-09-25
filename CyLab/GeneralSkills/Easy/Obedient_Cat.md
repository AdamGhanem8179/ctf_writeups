# picoCTF – Obedient Cat Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Obedient Cat

* **Category:** General Skills

* **Points:** 5

* **Date:** 9/25/2026

* **Flag:** academy{s4n1ty_v3r1f13d\_........}

## TL;DR (Abstract)

This foundational challenge serves as a sanity check for basic command-line file manipulation. After downloading the challenge file named `flag`, the Unix utility `cat` was executed (`cat flag`) to concatenate and print the contents of the file directly to standard output, immediately revealing the flag in plain text.

## Challenge Description

> This file has a flag in plain sight (or do we mean in the shell?). Download the flag file and see if you can extract it!

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Download the target file provided by the challenge instance:

```
wget https://.../flag
# or curl -O https://.../flag

```

Inspect the downloaded file type:

```
file flag

```

Output:

```
flag: ASCII text

```

The utility confirms that the file is an uncompressed, plain ASCII text file.

### 2. Formulating the Solution

In Unix-like operating systems, the standard utility `cat` (short for concatenate) is used to read sequential files and write them directly to standard output. Because the contents are unencrypted plain text, running `cat` against the file will directly display the contents on the terminal screen.

### 3. Execution & Flag Capture

Execute `cat` targeting the file:

```
cat flag

```

Terminal Output:

```
academy{s4n1ty_v3r1f13d_........}

```

The flag is printed directly to the terminal shell without requiring any decryption or further parsing.

## Remediation & Key Takeaways

* **Standard File Inspection:** `cat` is one of the most fundamental utilities for inspecting smaller text files in Linux/Unix environments.

* **Paging Large Outputs:** For longer files where `cat` would scroll past readable terminal buffers, interactive pagers such as `less` or `more`, or head/tail utilities (`head -n 20`, `tail -n 20`), are preferred.

* **Binary File Caution:** Always inspect unknown files using `file` prior to running `cat`, as dumping non-text binary streams directly to the shell can corrupt terminal state and character mappings.
