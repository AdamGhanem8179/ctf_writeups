writeup_content = """# Write-Up: Trust But Verify

**Tags:** `AI`, `LLM Security`, `Verification`, `CyLab Security Academy`, `picoCTF`, `Beginner`

---

## TL;DR

> **Trust But Verify** is an introductory interactive narrative challenge where an AI assistant confidently hands you snippets of code, citations, and analytical claims. While the AI presents itself as fully authoritative, taking its responses at face value leads to broken builds, fictional citations, and subtle security oversights. By systematically refusing to blindly accept the AI's outputs—manually checking each claim, auditing generated logic, and enforcing verification gates—we uncover the hidden pitfalls of LLM hallucinations and recover the final flag. Always audit what your models generate.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Trust But Verify |
| **Category** | Artificial Intelligence / Ethics & Foundations |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 9/8/2026 |

### Description

> *Play through an AI ethics interactive fiction where confident AI outputs can be wrong, subtly wrong, or almost-right. Verify claims, code, and citations to learn practical habits for safe AI-assisted work. Connect with netcat:*
>
> `$ nc <instance-host> <instance-port>`

---

## Thought Process & Initial Analysis

When approaching this challenge, the objective was not to exploit a low-level memory corruption vulnerability or crack a cryptographic cipher, but to navigate an **interactive fiction engine simulating an AI-assisted engineering workflow**.

Large Language Models (LLMs) are notorious for **hallucinations**—synthesizing information that sounds technically plausible and linguistically authoritative, yet contains fabricated imports, invalid library versions, broken syntax, or completely made-up academic references.

The core prompt gave a clear directive: **Verify claims, code, and citations.**

---

## Step-by-Step Walkthrough

### 1. Establishing the Session

Using our local Ubuntu terminal environment, we used Netcat (`nc`) to initiate the text stream with the remote challenge daemon:


### 2. Choosing the recheck ooption 

Kept on rechecking and verifying all the data that the ai gave us till we reached the end 

```
nc aureolin-pixie.cylabacademy.net 54898
