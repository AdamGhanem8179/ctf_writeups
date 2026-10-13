# CyLab – useless Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** useless

* **Category:** Linux / General Skills

* **Points:** 50

* **Date:** 10/13/2026

* **Flag:** academy{us3l3ss_ch4ll3ng3_3xpl0it3d_....}

## TL;DR (Abstract)

The challenge hints at a command or manual page named `useless`, but a standard `man` lookup fails. By executing a system-wide search using the `find` command, a compressed file related to the challenge is located. Using `zcat` to read the contents of the `.gz` file directly reveals the hidden flag.

## Challenge Description

> Read the manual. Wait, where did it go? Find the "useless" file and see what it contains.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge name and standard CTF tropes suggest looking for a manual page or executable named `useless`. The first logical step is to attempt to read its manual entry:

```bash
man useless
```

This returns no manual entry, indicating the file is missing from the standard `$MANPATH` directories or is hidden elsewhere on the system.

### 2. System-Wide Search

Since the file's exact location is unknown, the `find` command is leveraged to search the entire root directory (`/`) for any file starting with "useless". Errors (like permission denied on inaccessible directories) are routed to `/dev/null` to keep the output clean:

```bash
find / -name "useless*" 2>/dev/null
```

This search successfully locates a compressed gzip file on the system (for example, `/path/to/useless.gz`).

### 3. Execution & Flag Capture

Because the located file is compressed with `gzip` (indicated by the `.gz` extension), standard text reading commands like `cat` will output unreadable binary data. Instead, `zcat` is used to decompress and read the file's contents directly to standard output:

```bash
zcat /path/to/useless.gz
```

Reading the decompressed contents spills the flag to the terminal.

Flag:

```text
academy{us3l3ss_ch4ll3ng3_3xpl0it3d_....}
```
