# CyLab – printer shares 2 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** printer shares 2

* **Category:** Network Exploitation / General Skills

* **Difficulty:** Hard

* **Date:** 10/13/2026

* **Flag:** academy{5mb_pr1nter_5h4re5_5ecure\_........}

## TL;DR (Abstract)

This challenge requires enumerating network services to find an exposed notes file containing a valid username. With the username in hand, a dictionary attack using the `rockyou.txt` wordlist is launched against the target's SMB (Server Message Block) service. Once the password is cracked, authenticated access via `smbclient` allows the exfiltration of the flag file.

## Challenge Description

> The office printer share has been locked down since the last incident, or so they think. Can you find a way back in and retrieve the flag?

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

The first step in attacking the target is enumerating the available services. Exploring the initial open directories or anonymous SMB shares reveals a document or text file containing some administrative `notes`.

Reading through these notes inadvertently leaks a valid internal **username** used by the system administrators or employees.

### 2. Brute-Force Dictionary Attack

With a known valid username, the next logical step is to attempt to crack their password. Since the challenge involves an SMB printer share, we can use an automated brute-forcing tool (such as `hydra` or `crackmapexec`) paired with the infamous `rockyou.txt` wordlist.

```
hydra -l <discovered_username> -P /usr/share/wordlists/rockyou.txt smb://<target_ip>

```

After iterating through the wordlist, the tool successfully finds a match and outputs the valid password for the user.

### 3. Execution & Flag Capture

Armed with both the username and the cracked password, we can now authenticate directly to the restricted SMB share using `smbclient`.

```
smbclient //<target_ip>/<share_name> -U <discovered_username>

```

After entering the cracked password at the prompt, we are dropped into the `smb:\>` interactive shell. Listing the directory contents reveals `flag.txt`. We use the `get` command to download it to our local machine:

```
smb: \> get flag.txt

```

Finally, reading the downloaded file locally reveals the flag:

```
cat flag.txt

```

Flag:

```
academy{5mb_pr1nter_5h4re5_5ecure_........}

```
