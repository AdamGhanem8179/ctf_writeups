# CyLab – Big Zip Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Big Zip

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/26/2026

* **Flag:** academy{gr3p_15_m4g1c_........}

## TL;DR (Abstract)

The challenge involves searching through an unzipped archive containing a large volume of directories and nested files. Using `grep` with recursive (`-r`) and line-number (`-n`) flags to match the flag prefix `academy`, the file containing the flag was immediately located and extracted directly from the terminal.

## Challenge Description

> Search through the extracted archive files to locate and recover the hidden flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

After decompressing the provided archive, the directory structure contains numerous subfolders and text files, making manual inspection impractical:

* **Target Pattern:** Known flag wrapper `academy`
* **Tool:** `grep` with recursive search enabled
* **Search Scope:** Current directory (`.`) and all child folders

### 2. Execution & Flag Capture

Recursively search all files and subdirectories for the pattern `academy`:

```bash
grep -rn "academy" .
```

Terminal Output:

```
./path/to/folder/file.txt:1:academy{gr3p_15_m4g1c_........}
```

Flag:

```
academy{gr3p_15_m4g1c_........}
```
