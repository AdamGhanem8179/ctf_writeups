# Natas Level 1 Write-up

## Step 0 - Challenge Info
* **CTF Name:** OverTheWire
* **Challenge Name:** Natas 1
* **Category:** Web Security / Web Exploitation
* **Difficulty:** Beginner
* **Date:** November 3, 2026
* **Flag:** `vsDOxoXyq3wckCP1ZmTZ71ng........`

## TL;DR (Abstract)
This challenge demonstrates that client-side restrictions, such as blocking the right-click menu via JavaScript, are ineffective security measures. The flag can easily be retrieved by using alternative methods to view the page source.

## Challenge Description
> You can find the password for the next level on this page, but right-clicking has been blocked!

## Thought Process & Walkthrough
### 1. Reconnaissance & Information Gathering
Similar to Level 0, the goal is to find the password hidden in the webpage. However, when attempting to right-click on the page to select "View Page Source", a JavaScript restriction prevents the context menu from appearing. 

### 2. Execution & Flag Capture
Since the restriction is only enforced on the client side through the mouse click event, it can be easily bypassed using standard browser keyboard shortcuts. 

By pressing `Ctrl + U` (or `Cmd + Option + U` on Mac), the browser opens the raw HTML source code directly, ignoring the JavaScript block. Alternatively, hitting `F12` opens the Developer Tools to inspect the DOM, or prefixing the URL with `view-source:` in the address bar achieves the same result.

Scanning the source code reveals the HTML comment containing the next password:
```html
<!--The password for natas2 is vsDOxoXyq3wckCP1ZmTZ71ng........ -->
```

Flag:
```
vsDOxoXyq3wckCP1ZmTZ71ng........
```

## Mitigation & Lessons Learned
* **Defense:** Never rely on client-side JavaScript (like disabling right-click, hiding elements, or disabling text selection) to protect sensitive information or enforce security. Attackers have full control over their browser environment and can easily bypass these superficial barriers.
* **Takeaway:** Always remember that you control the client. If a web application tries to restrict your UI interactions, use developer tools, keyboard shortcuts, or command-line tools like `curl` to interact with the raw data directly.
