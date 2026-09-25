# picoCTF – First Grep Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** First Grep

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{grep_is_good_to_find_things_........}

## TL;DR (Abstract)

The challenge presents a large text file filled with thousands of lines of clutter and random character strings designed to conceal a flag. Rather than searching manually, the standard Unix regular expression utility `grep` was used with extended regex and match-only flags (`grep -oE '[A-Za-z0-9_]+\{[^}]*\}' file`) to extract the exact flag pattern directly from the file.

## Challenge Description

> Can you find the flag in file? This would be really tedious to look through manually, something tells me there is a better way.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the target file using standard file utilities:

```
file file
wc -l file
```

The output shows that `file` is an ASCII text document containing thousands of lines of pseudo-random text and noise. Browsing through the text with `cat` or `less` is impractical due to the volume of data.

### 2. Formulating the Solution with Regular Expressions

Knowing standard CTF flag formats follow a convention of an identifier followed by curly braces containing arbitrary text (`prefix{content}`), we can isolate the pattern using `grep`:

* `-E` enables Extended Regular Expressions (ERE).
* `-o` outputs **only** the matched parts of matching lines rather than printing entire noisy lines.
* The pattern `'[A-Za-z0-9_]+\{[^}]*\}'` matches:
  * `[A-Za-z0-9_]+`: One or more alphanumeric or underscore characters (e.g., `academy` or `picoCTF`).
  * `\{`: An opening curly brace literal.
  * `[^}]*`: Any number of characters that are not a closing brace.
  * `\}`: A closing curly brace literal.

### 3. Execution & Flag Capture

Execute the regex search directly against the file:

```
grep -oE '[A-Za-z0-9_]+\{[^}]*\}' file
```

Terminal Output:

```
academy{grep_is_good_to_find_things_........}
```

The expression strips away all surrounding text and noise, returning only the intact flag string.

## Remediation & Key Takeaways

* **Regex Pattern Extraction:** Using `grep -oE` allows precise extraction of targeted substrings (tokens, hashes, flag formats) without dumping surrounding clutter to the screen.
* **Format-Agnostic Matching:** Using general patterns like `[A-Za-z0-9_]+\{[^}]*\}` enables flag extraction even when the exact prefix (`picoCTF`, `academy`, `ctf`, etc.) is varied or unknown.
* **Basic Text Searching:** For simpler searches where the flag prefix is known in advance, straightforward string queries like `grep "academy{" file` or `grep -i "flag" file` can achieve identical results with less syntax overhead.
