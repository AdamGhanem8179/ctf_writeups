# Bandit Level 14 → Level 15

## 1. Objective

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was cat /etc/bandit_pass/bandit14 (told to me in level 13)  
• Then to go to port 30000 I used nc localhost 30000 then inputed the password so I got the password for level 15 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo  

---

## 4. Execution

Commands
cat /etc/bandit_pass/bandit14
nc localhost 30000


Explanation  
Explain:  
• nc short for netcat is a toold to connect to a port it weorks as nc host port  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Connecting to a port  

---

## 7. Lessons Learned

Sometime u need to talk to ports not always files or SSH  

---

## 8. Credential (Password)

Level 14 : MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS  
Level 15 : 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
