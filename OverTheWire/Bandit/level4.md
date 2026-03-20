# Bandit Level 4 → Level 5

## 1. Objective

The password for the next level is stored in the only human-readable file in the inhere directory. 

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (Ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First I entered the inhere file using cat  
• Then I saw I have many files and they start with – so I used file ./*  
• Then I got a list of the files and what they are made of so I searched for the one with ASCII  
• Finally I read it with cat and got the password  

---

## 4. Execution

Commands

```
ls  
cat  
file ./*
```

Explanation  
Explain:  
• File gives you information about the file and * selects all and ./ tells the terminal this is not a command it’s the file name  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Content search  

---

## 7. Lessons Learned

Checking what a file is made up of saved a lot of time  

---

## 8. Credential (Password)

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```
