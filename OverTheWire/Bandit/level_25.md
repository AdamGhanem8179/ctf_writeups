# Bandit Level 25 → Level 26

## 1. Objective

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing i did was get the sshkey then save it locally in a temp file  
• Then checked the environment how is it working it was like the more  
• So I made the screen small to get the effect of more then pressed v and switched it back to bash  

---

## 4. Execution

Commands
```
cat bandit26.sshkey
nano bandit26.sshkey
chmod 600 bandit26.sshkey
ssh bandit26@bandit.labs.overthewire.org
 -p 2220 -i bandit26.sshkey
:set shell=/bin/bash
:shell
```

---

## 5. Result

• Got the password for level 26  

---

## 6. Key Concepts

What is vi  

---

## 7. Lessons Learned

Sometimes its outside the terminal  

---

## 8. Credential (Password)
```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```
