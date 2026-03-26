# Bandit Level 18 → Level 19

## 1. Objective

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH. 

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was log in normally and i got the byebye message which was a hint in level 18   
• So then I knew I can enter directly but to get the password (they told us its in readme)  
• I used the cat in the same line while logging in  

---

## 4. Execution

Commands
ssh bandit18@bandit.labs.overthewire.org -p 2220 “cat readme”
Explanation  
Explain:  
• Diff is used to check the difference between these 2 files  

---

## 5. Result

• Got the password for level 19  

---

## 6. Key Concepts

• Using commands in par with signing in  

---

## 7. Lessons Learned

You can execute commands in par with joining which will bypass some commands that would force log you out  

---

## 8. Credential (Password)
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
