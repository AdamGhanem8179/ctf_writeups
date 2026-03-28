# Bandit Level 22 → Level 23

## 1. Objective

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.
Commands you may need to solve this level
cron, crontab, crontab(5) (use “man 5 crontab” to access this)

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing i did was enter /etc/cron.d/ then use ls to see whats inside  
• Since I need to reach level 23 I used cat on the file containing 23  
• Then I got how it works and cat /usr/bin/cronjob_bandit23.sh  
• After that since I want level 23 I gave it echo I am user bandit23 | md5sum  
• After I got the hashed file I used the location they gave me with the hashed file cat /tmp/8ca319486bfbbc3663ea0fbe81326349  -  

---

## 4. Execution

Commands
```
echo I am user bandit23 | md5sum
cat /tmp/8ca319486bfbbc3663ea0fbe81326349 -
```

Explanation  
Explain:  
• This level was the same as before where I navigated to get the password  

---

## 5. Result

• Got the password for level 23  

---

## 6. Key Concepts

Understanding better about how I can read cron and use it to my advantage

---

## 7. Lessons Learned

An attacker should first understand how a system generates the file paths he can access sensitive data

---

## 8. Credential (Password)
```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
