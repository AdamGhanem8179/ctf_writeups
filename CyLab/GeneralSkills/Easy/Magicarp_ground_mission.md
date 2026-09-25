# picoCTF – Magikarp Ground Mission Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Magikarp Ground Mission

* **Category:** General Skills

* **Points:** 30

* **Date:** 9/25/2026

* **Flag:** academy{xxsh_0ut_0f_//4t3r_.........}

## TL;DR (Abstract)

After establishing an SSH connection to the challenge target, the flag was discovered split across multiple files placed in distinct directories across the filesystem. By utilizing standard directory navigation commands (`cd`, `ls`) and outputting file contents via `cat`, all three flag fragments were located, inspected, and concatenated into the full flag string.

## Challenge Description

> Do you know how to move between directories and read files in the shell? Connect to the instance to find the flag fragments.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connect to the provided challenge instance using SSH:

```
ssh ctf-player@challenge.picoctf.net -p <port>
```

Listing files in the initial landing directory reveals the first fragment alongside a set of instructions:

```
ls -la
```

Target files found:
* `1of3.flag.txt`
* `instructions-to-2of3.txt`

### 2. Reading the First Fragment & Instructions

Display the contents of the first fragment:

```
cat 1of3.flag.txt
```

Terminal Output:

```
academy{xxsh_
```

Read the destination instructions for the second part:

```
cat instructions-to-2of3.txt
```

The file directs navigation to the root directory `/`.

### 3. Navigating to Root Directory

Change directory to `/` and list directory contents:

```
cd /
ls -la
```

Read the second fragment and the next instruction file:

```
cat 2of3.flag.txt
cat instructions-to-3of3.txt
```

Terminal Output:

```
0ut_0f_
```

The instructions specify moving to the user's home directory `~`.

### 4. Retrieving the Final Fragment & Flag Capture

Change directory to the home folder:

```
cd ~
ls -la
```

Read the third and final flag fragment:

```
cat 3of3.flag.txt
```

Terminal Output:

```
//4t3r_.........}
```

Combining the fragments sequentially (`academy{xxsh_` + `0ut_0f_` + `//4t3r_.........}`) completes the flag:

```
academy{xxsh_0ut_0f_//4t3r_.........}
```

## Remediation & Key Takeaways

* **Filesystem Traversal:** The `cd` command navigates file trees; absolute paths like `/` refer to system root, while `~` resolves to the current user's personal home directory.
* **Directory Enumeration:** Running `ls -la` ensures hidden dotfiles, permissions, and directory structures are fully visible.
* **Stream Concatenation:** `cat` outputs file streams directly to stdout without launching interactive editors, making it suitable for rapid flag inspection.
