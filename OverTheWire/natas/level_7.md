# Natas Level 7 Write-up

## Step 0 - Challenge Info
* **CTF Name:** OverTheWire Natas
* **Challenge Name:** Level 7 to Level 8
* **Category:** Web Exploitation / Local File Inclusion (LFI)
* **Difficulty:** Beginner
* **Date:** 2026-11-11
* **Flag:** `ugXL95KQmUAJJj6bMezOlBND........`

## TL;DR (Abstract)
Exploited a Local File Inclusion (LFI) vulnerability by manipulating a URL parameter. A hidden HTML comment in the source code provided the exact file path to the next level's password, which was then retrieved by injecting the path into the vulnerable parameter.

## Challenge Description
> The webpage features a simple navigation menu. Inspecting the source code reveals a hidden developer comment containing the absolute path to the password for the next level. The URL structure suggests that pages are being loaded dynamically via a `page` parameter.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering
Clicking around the site's navigation menu revealed that the URL changes dynamically, such as `?page=home` or `?page=about`. Viewing the page's HTML source code exposed a leftover developer comment:
```html
<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->
```

### 2. Exploiting Local File Inclusion (LFI)
The combination of the `page` parameter controlling what gets loaded and the hint pointing to a specific internal file indicated a Local File Inclusion (LFI) vulnerability. The web application is likely using a PHP function like `include()` or `file_get_contents()` directly on the user-supplied input without sanitizing it.

### 3. Execution & Flag Capture
To exploit this, I replaced the intended page name in the URL with the absolute path provided in the hint:
```
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

The server processed the request and displayed the contents of the password file directly on the page, revealing the flag:
```
ugXL95KQmUAJJj6bMezOlBND........
```

## Mitigation & Lessons Learned
* **Defense:** Never pass unsanitized user input directly to file inclusion or file reading functions. Implement an allowlist (whitelist) approach where only specific, hardcoded filenames (e.g., `home.php`, `about.php`) are permitted. Alternatively, use an index-based routing system where the parameter is an ID rather than a file path.
* **Takeaway:** Always inspect the source code for forgotten developer comments, as they often leak sensitive architectural information. Additionally, anytime a URL parameter dictates which file is loaded, it is a prime target for LFI or Directory Traversal testing.
