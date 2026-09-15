# CyLab 2026 – Log Hunt Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Log Hunt
* **Category:** Forensics / General Skills
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{us3_y0urlinux_sk1lls_........}

---

## TL;DR (Abstract)
The challenge provides a dense collection of system, application, or web access log files containing thousands of event entries. Finding the hidden secret manually is impractical due to the high volume of noise. By leveraging native Linux command-line text processing utilities (such as `grep`, `find`, or `awk`) to search recursively across log directories and filter for standard flag signatures (`picoCTF{`), the relevant entry is rapidly extracted, isolating the challenge flag.

---

## Challenge Description
> An unauthorized event was recorded somewhere inside the system logs. Utilize your Linux command-line filtering and log analysis skills to hunt through the records and extract the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Inspect the extracted challenge workspace or provided log archive:

ls -la

The directory contains multiple log files (or nested subdirectories like `/var/log/` or application audit files) containing extensive activity records:

total 4820
drwxr-xr-x 2 ctf ctf    4096 Sep 15 10:00 .
drwxr-xr-x 4 ctf ctf    4096 Sep 15 09:50 ..
-rw-r--r-- 1 ctf ctf 1824110 Sep 15 09:55 access.log
-rw-r--r-- 1 ctf ctf 2149582 Sep 15 09:58 auth.log
-rw-r--r-- 1 ctf ctf  953401 Sep 15 09:59 syslog

### 2. Searching & Filtering Log Files
Rather than reading through thousands of lines manually, apply standard Linux string searching tools. Because picoCTF flags use a known flag format (`picoCTF{...}`), run a case-insensitive recursive search across all files in the current directory:

grep -rni "picoCTF" .

Alternatively, if searching within compressed archives or deep directory trees:

zgrep -rn "picoCTF" . 2>/dev/null

### 3. Flag Capture
The search utility isolates the exact line and file where the string was recorded:

auth.log:1482:Sep 15 09:58:12 server sudo: pam_unix(sudo:session): session opened for user flag_service by (uid=0) picoCTF{us3_y0urlinux_sk1lls_........}

The captured flag:

picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}

---

## Remediation & Key Takeaways
* **Master Linux Text Filtering Tools:** Command-line utilities like `grep`, `ripgrep`, `awk`, `sed`, and `sort | uniq` are indispensable for rapidly cutting through noise in forensic artifact analysis.
* **Prevent Credential & Sensitive Data Leakage in Logs:** Systems must be configured to sanitize user input and environment variables before logging to prevent sensitive tokens, passwords, or flags from being written to persistent log files.
* **Centralized Log Management (SIEM):** In production environments, aggregate logs into structured indexing engines (e.g., Elasticsearch, Splunk, Graylog) where automated alert rules and regex queries can identify anomalies and sensitive data exposures instantly.
