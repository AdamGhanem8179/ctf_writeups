# picoCTF – Password Profiler Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Password Profiler
* **Category:** Cryptography / OSINT / Password Cracking
* **Points:** 100
* **Date:** 9/18/2026
* **Flag:** picoCTF{Aj_........}

---

## TL;DR (Abstract)
The challenge provides background details or personal information about a target user that must be leveraged to crack an encrypted archive, hash, or password-protected service. By running the Common User Passwords Profiler (`cupp.py`) in interactive mode and inputting the provided profile details (names, dates, and related keywords), a custom targeted wordlist was generated. Passing the generated wordlist to the target script/service successfully matched the credentials and revealed the flag.

---

## Challenge Description
> Profile the target! Gather the provided intelligence, craft a personalized dictionary using profiling tools, and crack the authentication mechanism to recover the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Inspect the challenge prompt to gather all personal identifiable information (PII) regarding the target. Key attributes include:
* Target name / nicknames
* Partner, pet, or company names
* Significant dates (birthdays, anniversaries)
* Custom keywords and special character permutations

### 2. Generating the Targeted Wordlist with CUPP
Using `cupp` (Common User Passwords Profiler), launch an interactive session to generate permutations based on the gathered profile:

python3 cupp.py -i

Fill in the target's information as prompted by the wizard:

[+] Insert the targets details:
> First Name: [Target First Name]
> Surname: [Target Surname]
> Nickname: [Target Nickname]
> Birthdate (DDMMYYYY): [Target Date]
...
[+] Do you want to add some special chars at the end of words? Y/N
[+] Do you want to add some random numbers at the end of words? Y/N

CUPP compiles and exports the customized candidate passwords to a `.txt` dictionary (e.g., `target.txt`).

### 3. Running the Cracking Script & Flag Capture
Run the provided challenge script against the generated dictionary to test the password candidates:

python3 crack.py -w target.txt

The script iterates through the wordlist, matches the correct permutation derived from the target's profile, and outputs the flag:

[+] Password found!
picoCTF{Aj_........}

---

## Remediation & Key Takeaways
* **Avoid Predictable PII-Based Passwords:** Passwords composed of names, birthdates, and basic character suffixes are highly vulnerable to targeted profiling attacks using tools like CUPP or Mentalist.
* **Adopt Passphrases or Random Strings:** Enforce lengthy, multi-word passphrases or fully randomized character sets that do not rely on personal background data.
* **Implement Rate Limiting & Lockouts:** Ensure authentication endpoints enforce exponential backoff or lockouts after repeated failed attempts to prevent automated dictionary attacks.
