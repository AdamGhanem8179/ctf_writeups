# picoCTF – Commitment Issues Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Commitment Issues
* **Category:** General Skills
* **Points:** 100
* **Date:** 9/18/2026
* **Flag:** picoCTF{s@n1t1z3_........}

---

## TL;DR (Abstract)
The challenge provides a Git repository where sensitive data was removed from the working tree in a recent commit to "sanitize" it. By using `git log` and `git diff` (or checking out the prior commit), the repository's commit history was traversed to view earlier versions of the modified file, exposing the flag before it was deleted.

---

## Challenge Description
> I accidentally committed something I shouldn't have, but I've already sanitized the repository. Can you find what was there before?

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Download and decompress the provided challenge archive:

unzip challenge.zip
cd drop-in

Inspect the current working directory:

ls -la
cat message.txt

The file currently in the working directory displays a clean/sanitized message (e.g., "TOP SECRET" or placeholder text) with no flag visible.

### 2. Inspecting the Commit Log
Check the commit history to see previous changes made to the repository:

git log

The output shows multiple commits, typically a "create" commit followed by a "sanitize" or "clean" commit:

commit 2b4c6e8... (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   ...

    clean flag

commit 1a3b5c7...
Author: picoCTF <ops@picoctf.com>
Date:   ...

    create flag

### 3. Comparing Revisions & Flag Capture
Inspect the differences between the current commit and the preceding one, or view the earlier version of the file using `git diff` or `git checkout`:

git diff HEAD~1 HEAD
# or
git checkout HEAD~1 message.txt && cat message.txt

Viewing the diff reveals the lines removed during the sanitization commit:

--- a/message.txt
+++ b/message.txt
@@ -1 +1 @@
-picoCTF{s@n1t1z3_........}
+TOP SECRET

The red/removed line directly exposes the original flag string.

---

## Remediation & Key Takeaways
* **Git Commit History Is Permanent:** Simply deleting or overwriting sensitive data in a subsequent commit does not sanitize a repository; all past states remain permanently retrievable in the `.git` directory.
* **Effective Repository Sanitization:** To truly purge sensitive information from version control history, use specialized rewriting tools such as `git-filter-repo` or BFG Repo-Cleaner, and force-push the purged branches.
* **Pre-commit Hooks:** Use tools like `gitleaks` or `trufflehog` with pre-commit hooks to block secrets and flags from being committed in the first place.
