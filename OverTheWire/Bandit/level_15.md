# Bandit Level 15 → Level 16

## 1. Objective

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was try to find a command like nc but has SSL/TLS so I found openssl  
• I used openssl s_client -connect localhost:30001  
• And then I manually entered the password but only got closed without the password for the next level  
• So I tried to give it the password using echo and piping and got done without the password  
• So this gave me an idea its reading it sooo fast because I placed the same code but In a different manor  
• So I finally decided to use sleep so I used grouping echo and sleep and then I piped it to keep it live  

---

## 4. Execution

Commands
( echo "8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo" ; sleep 2 ) | openssl s_client -connect localhost:30001


Explanation  
Explain:  
• Sleep is used here to keep the pipe live so it wouldn’t close so fast and will give me the password  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Controlling input  

---

## 7. Lessons Learned

I must adapt my tool depending on the protoco  

---

## 8. Credential (Password)
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
