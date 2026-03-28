# Bandit Level 27 → Level 28

## 1. Objective

There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
From your local machine (not the OverTheWire machine!), clone the repository and find the password for the next level. This needs git installed locally on your machine.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was clone the repo then I entered the repo  
• After that I read the README where I got the password  

---

## 4. Execution

Commands
```
git clone ssh://bandit27-git@bandit.labs.overthewire.org
:2220/home/bandit27-git/repo
ls
cd repo
ls
cat README
```

---

## 5. Result

• Got the password for level 28  

---

## 6. Key Concepts

Git uses SSH for authentication  

---

## 7. Lessons Learned

Git can pull code from any server and its not just for github  

---

## 8. Credential (Password)
```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```
