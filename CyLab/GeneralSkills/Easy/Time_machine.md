# picoCTF – Time Machine Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Time Machine
* **Category:** General Skills
* **Points:** 100
* **Date:** 9/18/2026
* **Flag:** picoCTF{t1m3m@ch1n3_........}

---

## TL;DR (Abstract)
The challenge provides a downloaded zip archive containing a Git repository where the current working tree appears empty or lacks the flag. By inspecting the repository's commit history with `git log`, the previous commit messages revealed the flag embedded directly within a past commit message.

---

## Challenge Description
> What was that file again? Look back in time to recover what was committed to the repository and find the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Download and extract the challenge archive containing the Git repository:

unzip challenge.zip
cd drop-in

Listing directory contents or checking the working directory with `ls -la` shows standard tracked files along with the `.git` directory:

ls -la

### 2. Inspecting Git History
Since Git maintains a complete cryptographic log of all historical revisions, author information, and commit messages, run `git log` to inspect past repository activity:

git log

### 3. Reviewing Commit Metadata & Flag Capture
The terminal outputs the chronological commit history:

commit a1b2c3d4e5f6... (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   ...

    picoCTF{t1m3m@ch1n3_........}

The commit message directly contains the flag string.

---

## Remediation & Key Takeaways
* **Git Commit Immutability:** Committing sensitive information, credentials, or keys directly into commit messages or tracked files persists permanently within the `.git` directory even if later removed or overwritten in the working tree.
* **Inspecting Version Control Artifacts:** When analyzing challenges or targets with exposed `.git` directories, always review `git log`, `git reflog`, `git diff`, and dangling commits (`git fsck --lost-found`).
* **Scrubbing Repositories:** Sensitive commits must be purged completely using tools like `git-filter-repo` or BFG Repo-Cleaner rather than simply making subsequent correction commits.
