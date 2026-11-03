# Natas Level 2 Write-up

## Step 0 - Challenge Info

* **CTF Name:** OverTheWire
* **Challenge Name:** Natas 2
* **Category:** Web Security / Web Exploitation
* **Difficulty:** Beginner
* **Date:** November 3, 2026
* **Flag:** `K30JrSRHzjxq3paUQuwozY4M........`

## TL;DR (Abstract)

This challenge highlights the risk of insecure server configurations, specifically enabling directory listing. By inspecting the page source and identifying a hidden directory path, an attacker can browse server files and locate sensitive information.

## Challenge Description

> There is nothing on this page.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

The rendered webpage claims there is nothing on the page, but as established in previous levels, the source code often tells a different story. Pressing `Ctrl + U` reveals the underlying HTML. 

While scanning the source code, line 15 stands out:
```html
<img src="files/pixel.png">
```
This indicates that there is a `files/` directory hosted on the web server.

### 2. Execution & Flag Capture

Since the image is stored in the `/files` directory, it's worth checking if the server allows us to view the contents of that directory directly. 

By appending `/files/` to the base URL in the browser (e.g., `http://natas2.natas.labs.overthewire.org/files/`), we discover that **Directory Listing** is enabled. Instead of being blocked, the server presents an "Index of /files" page showing all the files stored in that folder.

One of the files listed is typically named `users.txt`. Clicking on this file reveals a plaintext document containing the username and password for the next level.

Flag:
```
K30JrSRHzjxq3paUQuwozY4M........
```

## Mitigation & Lessons Learned

* **Defense:** Always disable directory listing (or directory indexing) on your web server. In Apache, for example, this can be done by adding `Options -Indexes` to the `.htaccess` file or server configuration. Furthermore, never store sensitive files (like credentials or internal text files) in publicly accessible web directories.
* **Takeaway:** Pay close attention to file paths and directories referenced in the source code (like images, scripts, or stylesheets). They can map out the directory structure of the application and reveal hidden folders that might be misconfigured.
