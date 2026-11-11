# Natas Level 9 Write-up

## Step 0 - Challenge Info
* **CTF Name:** OverTheWire Natas
* **Challenge Name:** Level 9 to Level 10
* **Category:** Web Exploitation / OS Command Injection
* **Difficulty:** Beginner
* **Date:** 2026-11-11
* **Flag:** `EgjlkzB6E8LJyf2Obt4q7q4e........`

## TL;DR (Abstract)
Exploited an OS Command Injection vulnerability by breaking out of an intended `grep` command. By using a semicolon (`;`) to chain commands and a hash (`#`) to comment out the rest of the backend query, the application was tricked into executing a `cat` command to read the password file for the next level.

## Challenge Description
> The application features a simple web form to search for words in a dictionary. The underlying PHP source code reveals that the user's search input is passed directly into a system command execution function (`passthru`) without any sanitization.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering
I started by testing the form with a standard word to see how it behaved, noting that it successfully returned matched text. Reviewing the provided PHP source code revealed the exact backend command being executed:
```php
passthru("grep -i $key dictionary.txt");
```
The `$key` variable represents the direct user input. Because it is neither sanitized nor enclosed in proper escape functions, it is vulnerable to command injection.

### 2. Crafting the Payload
Knowing the structure of the backend command and the location of the target passwords from previous levels (`/etc/natas_webpass/natas10`), I crafted a payload to manipulate the executed command. 

My payload: `; cat /etc/natas_webpass/natas10 #`

* `;` (Semicolon): Acts as a command separator in Linux, terminating the initial `grep` command.
* `cat /etc/natas_webpass/natas10`: The injected command used to read the target password file.
* `#` (Hash): Acts as a comment character in the shell, effectively nullifying the trailing ` dictionary.txt` part of the original hardcoded string so it doesn't cause a syntax error.

### 3. Execution & Flag Capture
When submitting the payload into the search field, the server evaluated the final command as:
```bash
grep -i ; cat /etc/natas_webpass/natas10 # dictionary.txt
```
The application executed the `cat` command and output the contents of the password file directly onto the webpage:
```
EgjlkzB6E8LJyf2Obt4q7q4e........
```

## Mitigation & Lessons Learned
* **Defense:** Never pass unsanitized user input directly to system execution functions like `passthru()`, `system()`, or `exec()`. If executing system commands is absolutely necessary, strictly validate the input and use built-in sanitization functions like `escapeshellarg()` or `escapeshellcmd()` in PHP to neutralize potential command chaining operators.
* **Takeaway:** Input fields that interact directly with the operating system are highly critical attack vectors. Understanding basic Linux shell operators (like `;`, `&&`, `|`, and `#`) is essential for identifying and exploiting command injection vulnerabilities.
