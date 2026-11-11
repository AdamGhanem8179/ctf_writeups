# Natas Level 10 Write-up

## Step 0 - Challenge Info

* **CTF Name:** OverTheWire Natas

* **Challenge Name:** Level 10 to Level 11

* **Category:** Web Exploitation / Argument Injection (Filter Bypass)

* **Difficulty:** Beginner

* **Date:** 2026-11-11

* **Flag:** `VUMQDmuITOEHzhviLE5V0VG9........`

## TL;DR (Abstract)

Bypassed a basic input filter that blocked standard command chaining characters (like `;`). By understanding that the backend `grep` command accepts multiple space-separated file paths, I injected the path to the target password file as a second argument and searched for a common vowel to output its contents.

## Challenge Description

> The application provides a dictionary search form similar to the previous level. However, inspecting the source code reveals that security restrictions have been added. A regular expression now blocks input containing characters typically used for command injection, such as semicolons (`;`) and pipes (`|`).

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

Reviewing the updated PHP source code revealed the following check:

```
if(preg_match('/[;|&]/', $key)) {
    print "Input contains an illegal character!";
} else {
    passthru("grep -i $key dictionary.txt");
}

```

Because the semicolon (`;`) used in Level 9 was now blocked, I could no longer terminate the `grep` command to start a new one like `cat`. I had to find a way to manipulate the existing `grep` command instead. 

### 2. Exploiting Command Arguments

I remembered that the `grep` command allows searching for a pattern across multiple files simultaneously by separating the file paths with spaces (e.g., `grep pattern file1 file2`). 

Since I had control over the `$key` variable, I could insert spaces to make `grep` search through both the intended `dictionary.txt` and my target file. 

My payload: `e /etc/natas_webpass/natas11`

* `e`: A common vowel that is highly likely to exist in the generated password.
* ` ` (Space): Separates the search pattern from the files.
* `/etc/natas_webpass/natas11`: The file I want `grep` to read.

### 3. Execution & Flag Capture

When submitting this payload, the backend executed the following command:

```
grep -i e /etc/natas_webpass/natas11 dictionary.txt

```

Because the `-i` flag makes the search case-insensitive, `grep` searched for the letter "e" or "E" in both the password file and the dictionary. It successfully found a match in the password file and printed the line to the screen:

```
/etc/natas_webpass/natas11:VUMQDmuITOEHzhviLE5V0VG9........

```

## Mitigation & Lessons Learned

* **Defense:** Filtering specific "bad" characters (a denylist approach) is rarely sufficient, as attackers can often find alternative ways to manipulate the command structure. To properly secure this, use PHP's `escapeshellarg()` function. This wraps the user input in single quotes, forcing the system to treat it as a single string/argument rather than executable code or multiple arguments.

* **Takeaway:** When command separators are blocked, look for "Argument Injection." Understanding the native behavior and syntax of the underlying command line tool (like `grep` accepting multiple files) can provide alternative pathways to exploit the vulnerability.
