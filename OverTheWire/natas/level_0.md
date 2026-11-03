# Natas Level 0 Write-up
## Step 0 - Challenge Info
* **CTF Name:** OverTheWire
* **Challenge Name:** Natas 0
* **Category:** Web Security / Web Exploitation
* **Difficulty:** Beginner
* **Date:** November 3, 2026
* **Flag:** `scfWG6qNEIdzqVyfRwEGXyNU........`

## TL;DR (Abstract)
This introductory web challenge demonstrates how sensitive information can be inadvertently exposed through client-side HTML comments. Obtaining the flag requires a simple inspection of the webpage's source code.

## Challenge Description
> You can find the password for the next level on this page.

## Thought Process & Walkthrough
### 1. Reconnaissance & Information Gathering
The challenge instructions indicate that the password for Natas1 is located directly on the Natas0 webpage. The rendered page simply displays a plain text message with no obvious input fields, forms, or complex mechanics.

### 2. Execution & Flag Capture
Since the password is not visible in the rendered UI text, the immediate next step is to inspect the underlying HTML code. 
```text
# Right-click the page and select "View Page Source" or press Ctrl+U.
```
Scanning through the raw HTML source code reveals an HTML comment intentionally left behind, which contains the credential for the next level.
```html
<!--The password for natas1 is scfWG6qNEIdzqVyfRwEGXyNU........ -->
```

Flag:
```text
scfWG6qNEIdzqVyfRwEGXyNU........
```

## Mitigation & Lessons Learned
* **Defense:** Never hardcode passwords, API keys, internal comments, or sensitive configuration details in front-end client-side HTML code, as this data is fully visible to anyone who visits the application.
* **Takeaway:** Viewing the page source is one of the most foundational and essential first steps when beginning reconnaissance for any web security assessment.
