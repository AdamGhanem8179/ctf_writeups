# Bandit Level 26 → Level 27

## 1. Objective

Good job getting a shell! Now hurry and grab the password for bandit27!

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was do the same thing I did in the previous level  
• Then I listed the files and saw bandit27-do which is a suid  
• So I used ./bandit27-do cat /etc/bandit_pass/bandit27  

---

## 4. Execution

Commands
```
ssh bandit26@bandit.labs.overthewire.org
 -p 2220 -i bandit26.sshkey
ls
./bandit27-do cat /etc/bandit_pass/bandit27
```

---

## 5. Result

• Got the password for level 27  

---

## 6. Key Concepts

Privilege escalation  

---

## 7. Lessons Learned

Chaining small permissions into full access  

---

## 8. Credential (Password)
```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```
