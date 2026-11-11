# Natas Level 6 Write-up

## Step 0 - Challenge Info
* **CTF Name:** OverTheWire Natas
* **Challenge Name:** Level 6 to Level 7
* **Category:** Web Exploitation
* **Difficulty:** Beginner
* **Date:** 2026-11-11
* **Flag:** `B1szg95UcTnrzwnF3i3TzYHl........`

## TL;DR (Abstract)
By inspecting the web page's source code, an included file directory was discovered. Accessing this referenced file directly via the URL exposed a hardcoded secret, which was then used in the main form to authenticate and retrieve the flag for the next level.

## Challenge Description
> The challenge requires submitting a specific "secret" into a web form to output the password for Natas 7. The underlying PHP source code is available to view on the page.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering
Reviewing the page source revealed a PHP snippet verifying the form input against a variable. The script pulled this variable by including an external file:
```php
include "includes/secret.inc";
```

### 2. Path Traversal & Exposure
Instead of attempting to brute-force the input field, the focus shifted to the referenced `includes/secret.inc` file. Because this file was stored within the public web directory without access restrictions, it could be accessed directly.

### 3. Execution & Flag Capture
Appending the directory path to the base URL (`http://natas6.natas.labs.overthewire.org/includes/secret.inc`) displayed the raw contents of the include file, revealing the secret string. 

Submitting this string back into the original web form successfully bypassed the check, revealing the flag:
```
Access granted. The password for natas7 is B1szg95UcTnrzwnF3i3TzYHl........
```

## Mitigation & Lessons Learned
* **Defense:** Keep sensitive information, configuration files, and secrets entirely outside the web root directory. If files must remain in the web root, configure the web server (e.g., Apache `.htaccess` or Nginx server blocks) to explicitly deny direct HTTP requests to `.inc`, `.env`, or configuration file extensions. 
* **Takeaway:** Never store sensitive information where users can view it. Client-side hiding is not security, and any accessible file on a web server will eventually be discovered if proper access control lists (ACLs) or routing restrictions are not enforced.
