# Bandit Level 1 → Level 2

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
• First thing I did was try to use cat - to escape it but it didn’t work
• So I thought of using another one which is cat ./-

---

## 4. Execution

```
ls 
cat ./-
```

Explanation
Explain:
• Cat reads a file and since the file conflicts with commands I parried it  with ./
• I expected it to work directly and give me the password

---

## 5. Result

• Successfully retrieved the password for the next level

---

## 6. Key Concepts

• Handling files with special filenames (-)
• Realizing that some commands wont treat - as a normal file but as a special input

---

## 7. Lessons Learned

Files with special names needs to be escaped before reading them

---

## 8. Credential (Password)

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```
