# Bandit Level 21 → Level 22

## 1. Objective

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing i did was enter /etc/cron.d/ then use ls to see whats inside  
• Since I need to reach level 22 I used cat on the file containing 22  
• Then I got how it works and cat /usr/bin/cronjob_bandit22.sh  
• After that I got the location of the password and read it  

---

## 4. Execution

Commands
```
Cat
ls
```

Explanation  
Explain:  
• This level was all about navigation and reading output  

---

## 5. Result

• Got the password for level 22  

---

## 6. Key Concepts

• Understanding what cron is  

---

## 7. Lessons Learned

The most important lesson is how to navigate in a new environment since I didn’t know anything about cron  

---

## 8. Credential (Password)
```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```
