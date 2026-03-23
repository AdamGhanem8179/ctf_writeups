# Bandit Level 9 → Level 10

## 1. Objective
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

---

## 2. Environment
• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology
Step-by-step approach:  
• First thing I did was use grep -o “=.*” data.txt  
• Then I got the error that is a binary file  
• So I added grep -ao “=.*” data.txt  

---

## 4. Execution

### Commands
    grep -ao “=.*” data.txt

### Explanation
Explain:  
• grep -a forces it to treat the file as a text so adding it and searching for the line that before it there is an = gave me a list 

---

## 5. Result
• Successfully retrieved the password for the next level  

---

## 6. Key Concepts
• Some commands depend on the file type to work so I need to force it to treat it like what it needs or find another way  

---

## 7. Lessons Learned
Forcing a file to be treated in another way is possible and favorited sometimes if the data isn’t corrupted  

---

## 8. Credential (Password)
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
