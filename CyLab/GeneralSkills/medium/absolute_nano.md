# CyLab – absolute nano Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** absolute nano

* **Category:** General Skills / Linux

* **Points:** 50

* **Date:** 10/1/2026

* **Flag:** academy{n4n0_411_7h3_w4y\_........}

## TL;DR (Abstract)

The challenge involves locating a restricted or nested flag file within an interactive Linux terminal environment. Listing directory contents with `ls -l` revealed the file structure and target paths. Using the command-line text editor `nano` and leveraging its built-in read-file shortcut (`Ctrl+R`), the target `flag.txt` was loaded into the editor buffer and read directly to retrieve the flag.

## Challenge Description

> Open files like a pro using the built-in tools. Can you read the hidden flag using nano?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the directory structure to identify available files, permissions, and paths:

```bash
ls -l
```

* **Observation:** The detailed file listing revealed the path or location pointing to `flag.txt`.

### 2. File Inspection with Nano (`Ctrl+R`)

Instead of opening the file directly via standard command-line redirection tools, the `nano` editor interface was used:

1. Launch the `nano` editor:

   ```bash
   nano
   ```

2. Inside the editor interface, activate the file insert/read function by pressing:

   ```text
   Ctrl + R  (Read File / Insert File)
   ```

3. Enter the relative or absolute path to the target file:

   ```text
   flag.txt
   ```
   *(or the exact directory path identified from `ls -l`)*

4. Press `Enter` to load the file contents directly into the active editor buffer.

### 3. Execution & Flag Capture

Reading the imported buffer in `nano` displays the flag text:

```text
academy{n4n0_411_7h3_w4y_........}
```

Flag:

```text
academy{n4n0_411_7h3_w4y_........}
```
