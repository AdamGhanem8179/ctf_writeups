# CyLab – printer shares 3 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** printer shares 3

* **Category:** Network Exploitation / General Skills

* **Difficulty:** Hard

* **Date:** 10/15/2026

* **Flag:** academy{5mb_pr1nter_5h4re5_r3v3r53\_........}

## TL;DR (Abstract)

Building upon the access gained in the previous challenge, this stage requires escalating privileges or gaining remote code execution (RCE). By uploading a reverse shell payload to the writable SMB share and triggering it, a connection is established back to the attacker machine, allowing us to read the final flag.

## Challenge Description

> The printer share might be secure, but the underlying system still has flaws. Can you pivot your access into a full reverse shell and grab the final flag?

## Thought Process & Walkthrough

### 1. Payload Generation

With write access to the SMB share confirmed from the previous challenge, the first step is to generate a reverse shell payload. Depending on the target system (Linux/Windows), a tool like `msfvenom` or a standard reverse shell script (Bash, Python, PHP, etc.) is created.

For example, generating a simple executable or script payload pointing back to our local machine's IP and listening port.

### 2. Uploading to SMB

Using the credentials cracked in "printer shares 2", we log back into the SMB share using `smbclient` and upload our malicious payload using the `put` command.

```
smbclient //<target_ip>/<share_name> -U <discovered_username>
smb: \> put reverse_shell.sh (or payload.exe)
```

### 3. Catching the Shell

Before triggering the payload, a netcat listener is started on our local machine to catch the incoming connection:

```
nc -lvnp 4444
```

Next, we find a way to trigger the uploaded file. This might involve interacting with a related web application, exploiting a scheduled task (cron job) that runs scripts from the share, or using Impacket's `psexec`/`smbexec` if we have sufficient privileges.

### 4. Execution & Flag Capture

Once the payload is triggered, the netcat listener catches the reverse shell connection, granting interactive command-line access to the target system. 

Navigating through the file system to the root or user directory reveals the target flag file.

```
cat /root/flag.txt
# or 
type C:\Users\Administrator\Desktop\flag.txt
```

Flag:

```
academy{5mb_pr1nter_5h4re5_r3v3r53_........}
```
