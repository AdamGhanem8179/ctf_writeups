# Bandit Level 3 → Level 4

## 1. Objective

The password for the next level is stored in a hidden file in the inhere directory.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (Ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First I used ls to check what I have  
• Then I entered the file inhere with cat  
• Then I used ls -a to get the hidden file  
• Finally I read it with cat and got the password  

---

## 4. Execution

Commands

```
ls -a  
cat
```

Explanation  
Explain:  
• Ls -a reads the hidden files also  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Hidden files  

---

## 7. Lessons Learned

A file can be hidden I should always check  

---

## 8. Credential (Password)

```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```
