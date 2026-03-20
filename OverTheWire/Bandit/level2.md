# Bandit Level 2 → Level 3

## 1. Objective

Find the password present inside file “-”

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (Ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was try to use cat –tab but it didn’t work  
• So I knew I should escape the spaces so I added -- “” --

---

## 4. Execution

```
ls  
cat -- “” --
```

Explanation  
Explain:  
• Cat reads a file and since the file conflicts with commands I parried it with --“” --

---

## 5. Result

• Successfully retrieved the password for the next level

---

## 6. Key Concepts

• Handling files with spaces

---

## 7. Lessons Learned

Filenames containing spaces must be handled properly using quotes or escape characters

---

## 8. Credential (Password)

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```
