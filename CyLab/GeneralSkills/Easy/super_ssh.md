# picoCTF – Super SSH Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Super SSH
* **Category:** General Skills / Network
* **Points:** 100
* **Date:** 9/18/2026
* **Flag:** picoCTF{s3cur3_c0nn3ct10n_........}

---

## TL;DR (Abstract)
The challenge tests fundamental remote access using the Secure Shell (SSH) protocol over a non-standard port. By executing `ssh` specifying the provided port, host, and username, accepting the remote host key fingerprint, and submitting the given password, a remote shell session was established. Upon successful authentication, the server printed the flag directly to the terminal banner.

---

## Challenge Description
> Connect to the remote server using the provided SSH credentials, authenticate securely, and retrieve the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
The challenge prompt provides connection details for a remote machine:
* **Host / Address:** `website.net`
* **Port:** `[Port]`
* **Username:** `[Username]`
* **Password:** `[Password]`

Standard SSH connections default to port 22, so the designated port must be explicitly specified using the `-p` switch.

### 2. Initiating the Secure Connection
Open a terminal and connect to the host using the specified port and user credentials:

ssh -p [port] [username]@website.net

When connecting to a host for the first time, OpenSSH prompts to verify the authenticity of the remote host key:

The authenticity of host '[website.net]:[port]' can't be established.
ED25519 key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes

Type `yes` to store the host key in `~/.ssh/known_hosts`.

### 3. Authenticating & Flag Capture
When prompted, provide the challenge password:

[username]@website.net's password: [password]

Upon successful authentication, the message of the day (MOTD) / login banner triggers and outputs the flag:

Welcome to the server!
picoCTF{s3cur3_c0nn3ct10n_........}

Connection to website.net closed.

---

## Remediation & Key Takeaways
* **SSH Port Configuration:** Always remember that `-p` flags in SSH client invocations allow targeting customized external listener ports when services do not run on TCP 22.
* **Host Key Verification:** Storing and checking host key fingerprints (`known_hosts`) ensures protection against Man-in-the-Middle (MitM) attacks during initial session handshakes.
* **Banner Exposure:** Avoid outputting sensitive credentials, system details, or keys directly within automated login banners or MOTD messages in production environments.
