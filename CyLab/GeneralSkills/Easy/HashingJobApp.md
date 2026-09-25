# picoCTF – HashingJobApp Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** HashingJobApp

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{4ppl1c4710n_r3c31v3d\_........}

## TL;DR (Abstract)

This challenge simulates a job application process that requires proving basic cryptographic knowledge. The interactive service prompts the user with a specific text string and waits for its MD5 hash to be submitted in return. By copying the provided word, hashing it using an MD5 application, and submitting the resulting hex digest back to the server, the application is "accepted" and the flag is revealed.

## Challenge Description

> If you want to hash with the best, beat this test! Connect to the service, read the word we give you, and send back its MD5 hash to prove your skills and get the job.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connect to the challenge instance (via `nc` or a web interface depending on the exact deployment). The server immediately issues a prompt similar to this:

```
Please input the MD5 hash of the text: "scrumptious"

```

The service gives us a string and halts, waiting for user input. If we input random text, the service terminates or rejects the application. 

### 2. Generating the Hash

The challenge explicitly requires an MD5 hash of the provided word. To solve this, the exact word provided by the prompt must be hashed without any extra spaces or newline characters.

Using an external hashing application (or an online MD5 generator):
* Input the exact string provided by the server.
* The application processes the text through the MD5 hashing algorithm.
* For a word like "scrumptious", the app outputs a 32-character hexadecimal string.

*(Note: In a Unix terminal, the exact equivalent command would be `echo -n "scrumptious" | md5sum`)*.

### 3. Execution & Flag Capture

Copy the generated 32-character MD5 hash from the hashing app and paste it back into the waiting challenge prompt:

```
Please input the MD5 hash of the text: "scrumptious"
> 25779ab76bc2959828d1e2e6b72a6b22
Correct! Application received.
academy{4ppl1c4710n_r3c31v3d_........}

```

Submitting the correct hash validates the input, and the service outputs the flag before closing the connection.

## Remediation & Key Takeaways

* **Understanding Hash Functions:** MD5 is a cryptographic hash function that produces a fixed-size 128-bit (32-character hex) hash value. Even a single character change in the input produces a drastically different output.
* **String Termination:** When generating hashes manually or via apps, it is critical to ensure no hidden newline (`\n`) or space characters are included in the input, as `hash("word")` and `hash("word\n")` will yield completely different results.
* **Automation for Speed:** While using a standalone app works for a single prompt, challenges that require hashing multiple strings quickly (within a time limit) require scripting, typically using Python's `hashlib` library and `pwntools` to handle the network socket automatically.
