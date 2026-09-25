# picoCTF – Tab, Tab, Attack Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Tab, Tab, Attack
* **Category:** General Skills
* **Points:** 20
* **Date:** 9/25/2026
* **Flag:** academy{l3v3l_up!_t4k3_4_r35t!_........}

---

## TL;DR (Abstract)
The challenge provides an archive containing deeply nested single-branch directories with long names. By utilizing shell tab-completion (`Tab` key) to rapidly traverse down each successive subdirectory without manually typing the paths, we locate a compiled Linux ELF binary (`fang-of-haynekhtnamet`). Executing the binary in terminal outputs the flag.

---

## Challenge Description
> Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: Addadshashanammu.zip.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Download and extract the challenge archive:

```bash
unzip Addadshashanammu.zip
```

The output reveals a long, cascading chain of single directories nested inside one another:

```text
Addadshashanammu/
└── Almurbalarammi/
    └── Ashalmimilkala/
        └── Assurnabitashpi/
            └── Maelkashishi/
                └── Onnissiralis/
                    └── Ularradallaku/
                        └── fang-of-haynekhtnamet
```

### 2. Navigating with Tab-Completion
Rather than typing each long, obscure directory name manually, we leverage terminal tab-completion. Because each directory contains only one child directory, pressing `Tab` automatically fills in the only unambiguous path.

* Start navigation:
  ```bash
  cd Add[Tab]/Alm[Tab]/Ash[Tab]/Ass[Tab]/Mae[Tab]/Onn[Tab]/Ula[Tab]
  ```
* Rapidly hitting `cd A` followed by successive `Tab` presses traverses straight to the innermost directory `Ularradallaku`.

### 3. Inspecting and Executing the Target File
Inside the final directory, inspect the contents:

```bash
ls -la
file fang-of-haynekhtnamet
```

The file command identifies it as a 64-bit ELF executable:

```text
fang-of-haynekhtnamet: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, not stripped
```

Ensure the binary has execution permissions and run it:

```bash
chmod +x fang-of-haynekhtnamet
./fang-of-haynekhtnamet
```

Terminal Output:
```text
*ZAP!* academy{l3v3l_up!_t4k3_4_r35t!_........}
```

---

## Remediation & Key Takeaways
* **Shell Productivity with Tab Completion:** Bash and Zsh auto-complete commands, file paths, and directory trees when unambiguous, drastically reducing typing errors and navigation time.
* **Alternative Shortcut Navigation:** Instead of recursive traversal, files nested in deep hierarchies can be quickly located or extracted directly using commands like `find . -type f` or `strings $(find . -type f) | grep -E "academy\{|picoCTF\{"`.
* **Safe Binary Execution:** Always verify untrusted binaries using `file` or inspect static strings (`strings <binary>`) before running them directly in your environment.
