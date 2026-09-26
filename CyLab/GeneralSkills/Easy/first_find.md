# CyLab – First Find Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** First Find

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/26/2026

* **Flag:** academy{f1nd_15_f457_........}

## TL;DR (Abstract)

The challenge requires locating a specific file hidden deep within a directory hierarchy. Using the Unix `find` command with the `-name` option quickly pinpoints the exact file path. Navigating to the directory and reading the file contents with `cat` reveals the flag.

## Challenge Description

> Find the target file hidden within the directories and extract the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The objective is to search the current working directory and its subdirectories to locate the target file:

* **Tool:** `find`
* **Search Root:** `.` (current working directory)
* **Goal:** Locate the file, navigate to its directory, and inspect its contents.

### 2. Execution & Flag Capture

Search for the file using the `-name` flag:

```bash
find . -name "*uber-secret.txt*"
```

Navigate to the directory returned by `find` and inspect the contents:

```bash
cd ./path/to/directory/
cat uber-secret.txt
```

Terminal Output:

```
academy{f1nd_15_f457_........}
```

Flag:

```
academy{f1nd_15_f457_........}
```
