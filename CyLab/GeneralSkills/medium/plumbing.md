# CyLab – plumbing Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** plumbing

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{digital_plumb3r\_........}

## TL;DR (Abstract)

The challenge exposes a remote network service that floods the connection with an immense amount of decoy text lines. By leveraging Unix I/O redirection and piping the raw output stream of Netcat into `grep` with fixed-string matching (`grep -aF 'academy{'`), the noise was instantly filtered out to isolate the hidden flag line.

## Challenge Description

> Sometimes you have to handle large streams of data. Can you pipe the output from this service to find the flag? Connect to the host and port provided.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connect to the challenge instance using Netcat:

```bash
nc <host> <port>
```

* **Observation:** The remote server immediately responds with hundreds or thousands of lines containing random filler text, fake tokens, and repeated strings.
* **Challenge:** Manually reading through or scrolling across the incoming network buffer is inefficient and prone to missing the flag.

### 2. Stream Filtering with Unix Pipes (`|`)

In Unix-like systems, stdout from one process can be redirected as stdin into another using the pipe (`|`) operator.

To filter the stream directly as data arrives:
* `grep`: Searches the standard input stream for matches.
* `-a` / `--text`: Treats binary or unusual incoming byte streams as plain text, preventing grep from aborting on non-printable bytes.
* `-F` / `--fixed-strings`: Treats the pattern as a fixed string rather than a regular expression for faster matching.

Command execution:

```bash
nc <host> <port> | grep -aF 'academy{'
```

### 3. Execution & Flag Capture

Running the piped command filters out all extraneous lines immediately and returns only the flag:

```text
academy{digital_plumb3r_........}
```

Flag:

```text
academy{digital_plumb3r_........}
```
