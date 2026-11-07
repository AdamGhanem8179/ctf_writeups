# Title Write-up

## Step 0 - Challenge Info
* **CTF Name:** OverTheWire Natas
* **Challenge Name:** Level 5 to Level 6
* **Category:** Web Exploitation
* **Difficulty:** Beginner
* **Date:** 2026-11-07
* **Flag:** 7mhjtShJAcld2NYbKHEadnhE.........

## TL;DR (Abstract)
Bypassing a broken access control mechanism by modifying an unauthenticated, client-side cookie from `loggedin=0` to `loggedin=1`.

## Challenge Description
> Access disallowed. You are not logged in.

## Thought Process & Walkthrough
### 1. Reconnaissance & Information Gathering
Inspecting the application state reveals that the server relies on a local cookie named `loggedin` to check authorization. By default, this cookie is passed to the user with a value of `0`. 

### 2. Execution & Flag Capture
Because the cookie is stored on the client side, the user has full control over its value and can manipulate it to trick the server into granting access. 

**Method 1: Browser Developer Tools**
1. Open the browser's Developer Tools.
2. Navigate to the **Application** (or Storage) tab, then select **Cookies**.
3. Locate the `loggedin` cookie.
4. Modify its value from `0` to `1`.
5. Refresh the page to bypass the restriction and reveal the password.

**Method 2: Terminal via cURL**
You can inject the forged cookie directly into the HTTP request using the `--cookie` parameter:
```bash
curl -u natas5:e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M --cookie "loggedin=1" http://natas5.natas.labs.overthewire.org
```

Flag:
```text
7mhjtShJAcld2NYbKHEadnhE.........
```

## Mitigation & Lessons Learned
* **Defense:** Never trust anything the user can edit or change the truth of, such as plaintext cookies or HTTP headers. To secure the application, keep track of who the user is and what access they have strictly on the server side. Issue a secure, randomized session ID upon a valid login, and validate permissions against that session for every restricted request.
* **Takeaway:** Client-side state management is inherently insecure for authentication. Always enforce access controls server-side.
