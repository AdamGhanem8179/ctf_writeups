# Natas Level 3 Write-up

## Step 0 - Challenge Info

* **CTF Name:** OverTheWire

* **Challenge Name:** Natas 3

* **Category:** Web Security / Web Exploitation

* **Difficulty:** Beginner

* **Date:** November 3, 2026

* **Flag:** `JDrPnuZAKyl6MkiqQGFIddrq........`

## TL;DR (Abstract)

This challenge demonstrates the risk of information disclosure through the `robots.txt` file. While intended to prevent search engines from indexing certain paths, this publicly accessible file can inadvertently reveal hidden directories to attackers.

## Challenge Description

> There is nothing on this page.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

Once again, looking at the rendered page yields no obvious clues. Opening the page source with `Ctrl + U` reveals an HTML comment left by the developer:

```html
<!-- No more information leaks!! Not even Google will find it this time... -->
```

The specific mention of "Google" is a major hint. Search engines like Google use automated web crawlers (spiders) to index websites. Websites communicate with these crawlers using a standardized file called `robots.txt`, which tells them which pages or directories they are allowed or disallowed from visiting. 

### 2. Execution & Flag Capture

Since `robots.txt` is always located at the root of a website, the next logical step is to navigate to:
`http://natas3.natas.labs.overthewire.org/robots.txt`

Viewing this file reveals the following configuration:
```
User-agent: *
Disallow: /s3cr3t/
```

The developer attempted to hide the `/s3cr3t/` directory from search engines, but in doing so, they explicitly told us exactly where the hidden "missed" location is. 

Navigating to `http://natas3.natas.labs.overthewire.org/s3cr3t/` reveals another directory listing (similar to Level 2). Inside, there is a `users.txt` file containing the password for the next level.

Flag:

```
JDrPnuZAKyl6MkiqQGFIddrq........
```

## Mitigation & Lessons Learned

* **Defense:** Never use `robots.txt` to hide sensitive directories or files. The `robots.txt` file is completely public and is one of the first places attackers look during reconnaissance. If a directory needs to be restricted, protect it with proper authentication and authorization controls, not just security by obscurity.
* **Takeaway:** When hints mention search engines or crawlers, immediately check the `robots.txt` file. It is a goldmine for discovering administrative panels, backup folders, and secret paths.
