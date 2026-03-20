# Bandit Level 5 → Level 6

## 1. Objective

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
• human-readable  
• 1033 bytes in size  
• not executable  

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (Ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First I entered the inhere file using cat  
• Then I saw I have many folders and inside them there is many files  
• So I used find with the information that I already have and got the path  
• Finally I read it using cat and the path  

---

## 4. Execution

Commands

```
ls  
find -type f -size 1033c ! -executable  
cat
```

Explanation  

• Find searches for something specific so I gave it type -f for file and 1033c aka 1033bytes and ! -executable as in not executable  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Content search  

---

## 7. Lessons Learned

I can input specific information to find that would make it easier  

---

## 8. Credential (Password)

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```
