# Title Write-up (cyber_writeup.docx)
## Step 0 - Challenge Info
* **CTF Name:** OverTheWire Natas
* **Challenge Name:** Level 4 to Level 5
* **Category:** Web Exploitation
* **Difficulty:** Beginner
* **Date:** 2026-11-07
* **Flag:** e4z2Noy3oqwPJUWzJH0dseN6........

## TL;DR (Abstract)
Bypassing an insecure access control mechanism by spoofing the HTTP Referer header to retrieve the password for the next level.

## Challenge Description
> Access disallowed. You are visiting from "" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/"

## Thought Process & Walkthrough
### 1. Reconnaissance & Information Gathering
The server explicitly requires incoming requests to originate from the Natas5 URL. Since the origin of a request is dictated by the `Referer` HTTP header—which is completely controlled by the client—it can be manipulated to bypass the restriction.

### 2. Header Spoofing (Adapted from Brute-Force Dictionary Attack)
Instead of brute-forcing, the solution requires crafting a request that manually defines the `Referer` header as `http://natas5.natas.labs.overthewire.org/`. 

### 3. Execution & Flag Capture
**Method 1: Terminal via cURL**
The `-e` flag allows you to set the referer directly from the command line:
```bash
curl -u natas4:JDrPnuZAKyl6MkiqQGFIddrqpvgOASth -e "http://natas5.natas.labs.overthewire.org/" http://natas4.natas.labs.overthewire.org
```

**Method 2: Burp Suite Interception**
By turning on Burp Suite's proxy, the GET request can be intercepted before it reaches the server. Manually adding the line `Referer: http://natas5.natas.labs.overthewire.org/` to the HTTP headers and forwarding the request bypasses the check.

Finally, reading the returned HTML payload locally reveals the flag:

Flag:
```text
e4z2Noy3oqwPJUWzJH0dseN6........
```

## Mitigation & Lessons Learned
* **Defense:** Do not depend on the referer as proof that someone had access and give it to them since it can be altered. Implement proper session management where a user logs in once and their permission is set securely. On each page where there is an asset to be protected, or to check permissions, validate access directly from that established login session instead of trusting client-side headers.
* **Takeaway:** Using tools like cURL and Burp Suite intercept highlights how trivially an attacker can manipulate HTTP requests, reinforcing that user-provided data should never be trusted for authorization checks.
