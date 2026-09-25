# picoCTF – Glitch Cat Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Glitch Cat

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{gl17ch_m3_n07_........}

## TL;DR (Abstract)

Connecting to the remote service using `nc` (netcat) outputs a Python-formatted string expression where portions of the flag are represented as ASCII hexadecimal evaluations via `chr(0x...)`. By piping or running the raw expression directly through the Python interpreter, the character codes are resolved into plain text and concatenated into the complete flag.

## Challenge Description

> Our flag printing service has started glitching! Can you reconnect and figure out what it's trying to say?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Establish a connection to the provided challenge server and port:

```
nc saturn.picoctf.net <port>
```

The service returns a single-line Python expression with string concatenation:

```
'academy{gl17ch_m3_n07_' + chr(0x62) + chr(0x31) + chr(0x37) + '........}'
```

### 2. Identifying the Encoding

* The output is formatted as a valid Python expression joined with `+`.
* Embedded characters are wrapped in `chr(0x...)`, which converts hexadecimal ASCII integer representations into printable characters.

### 3. Execution & Flag Capture

Evaluate the string directly using the Python 3 CLI:

```
python3 -c "print('academy{gl17ch_m3_n07_' + chr(0x62) + chr(0x31) + chr(0x37) + '........}')"
```

Alternatively, evaluate the raw network stream directly in a single pipe:

```
nc saturn.picoctf.net <port> | python3 -c "import sys; print(eval(sys.stdin.read().strip()))"
```

Terminal Output:

```
academy{gl17ch_m3_n07_........}
```

The reconstructed output yields the final flag:

```
academy{gl17ch_m3_n07_........}
```

## Remediation & Key Takeaways

* **Hexadecimal ASCII Conversion:** In Python, `chr()` maps numeric ASCII values (decimal or hex with `0x`) back into character literals.
* **Stream Evaluation:** Piping terminal network tools like `nc` directly into dynamic interpreters allows for rapid sanitization and decoding during active challenges.
