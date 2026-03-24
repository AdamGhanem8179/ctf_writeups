# Bandit Level 13 → Level 14

## 1. Objective
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level,
you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels,
and find out how to use the key for this level.

---

## 2. Environment
• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (Ubuntu)

---

## 3. Methodology
Step-by-step approach:
• Retrieved the private SSH key from bandit13  
• Saved the key locally in a file  
• Fixed permissions to make it usable  
• Used the key to authenticate and log into bandit14  

---

## 4. Execution

Commands:
chmod 600 key  
ssh -i key bandit14@bandit.labs.overthewire.org -p 2220  
cat /etc/bandit_pass/bandit14  

Explain:
• chmod 600 ensures the key has the correct permissions so SSH accepts it  
• ssh -i key logs in using the private key instead of a password  

---

## 5. Result
• Successfully logged into bandit14 using the private SSH key  

---

## 6. Key Concepts
• SSH key-based authentication  
• Importance of file permissions  
• Using keys instead of passwords for secure access  

---

## 7. Lessons Learned
I learned that SSH keys must be correctly formatted and have proper permissions or they will not work
Also authentication can depend on where you connect from (local vs remote) and small mistakes in setup can break the process

---

## 8. Credential (Password)
