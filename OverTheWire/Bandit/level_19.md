# Bandit Level 19 → Level 20

## 1. Objective

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was search for the setuid file using find . -perm -4000  
• Then I got ./bandit20-do  
• So I just typed it and got how to use it   
• Then I used ./bandit20-do cat /etc/bandit_pass/bandit20 and got the password  

---

## 4. Execution

Commands
```
find . -perm -4000
./bandit20-do
./bandit20-do cat /etc/bandit_pass/bandit20
```

Explanation  
Explain:  
• To find the setuid I need to search for files with permission 4000 (4000 is for setuid)  
• Using the file I got it tells you how to run it   

---

## 5. Result

• Got the password for level 20  

---

## 6. Key Concepts

• No need to think what how can I access the file but I can focus on searching for a file that can access it instead  

---

## 7. Lessons Learned

I can use files that would execute commands that require higher levels   

---

## 8. Credential (Password)
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
