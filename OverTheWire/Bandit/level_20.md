# Bandit Level 20 → Level 21

## 1. Objective

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
NOTE: Try connecting to your own network daemon to see if it works as you think

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing i did was find the setuid then I saw how to use it  
• Then I opened another terminal where in terminal 1 I was listening and in terminal 2 I pinged a random port  
• After that I entered the password for level 20 inside terminal 1 and it sent the password for level 21  

---

## 4. Execution

Commands

```
find . -perm -4000
/home/bandit20/suconnect
nc -l -p 1234
```

Explanation  
Explain:  
• 2 terminals where used so one will listen while the other pings it and nc -l was used to listen to the specified port -p 1234  

---

## 5. Result

• Got the password for level 21  

---

## 6. Key Concepts

• Controlling the server in a client server communication  

---

## 7. Lessons Learned

Its something like SSRF but for systems  

---

## 8. Credential (Password)
```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```
