# CyLab – Dont_You_Love_Banners Write-up

## Step 0 - Challenge Info

- **CTF Name:** CyLab

- **Challenge Name:** Dont_You_Love_Banners

- **Category:** Linux / General Skills

- **Points:** 50

- **Date:** 10/13/2026

- **Flag:** academy{b4nn3r_gr4bb1n9_su((3sfu11y_........}

## TL;DR (Abstract)

The challenge involves exploiting how a system or script reads a banner file. By removing the default `banner` file and replacing it with a symbolic link (symlink) pointing to the root directory (or the root flag file), we can trick the system into serving the contents of the restricted file, revealing the flag.

## Challenge Description

> Banners are a great way to welcome users to a server, but are they secure? See if you can grab the flag. 

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

After connecting to the challenge server, checking the current directory reveals a file named `banner`. This file is likely read and displayed to the user upon logging in or interacting with a specific service. 

Because we have write permissions in our current directory, we can manipulate this file to perform a symlink attack.

### 2. Exploitation & Symlink Creation

The goal is to read a restricted flag file located in the root directory (e.g., `/root/flag.txt` or `/`). 

First, we remove the existing banner file:

```bash
rm banner
```

Next, we create a symbolic link named `banner` that points directly to the target file in the root directory:

```bash
ln -s /root/flag.txt banner
# (Alternatively, linking to the root folder: ln -s / banner)
```

### 3. Execution & Flag Capture

With the symlink in place, we trigger the service or script that reads the `banner` file. Instead of reading the original welcome message, the system follows the symlink and reads the contents of the restricted root file.

The output spills the contents of the file, revealing the flag.

Flag:

```text
academy{b4nn3r_gr4bb1n9_su((3sfu11y_........}
```
