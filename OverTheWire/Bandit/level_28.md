# Bandit Level 28 → Level 29

## 1. Objective

There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220. The password for the user bandit28-git is the same as for the user bandit28.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was exactly the same as the previous level  
• Then when I found it censored I looked at the logs  
• Found a suspicious log so I checked it  

---

## 4. Execution

Commands
```
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
cat README.md
git log
git show 8b7c651b37ce7a94633b7b7b7c980ded19a16e4f
```

---

## 5. Result

• Got the password for level 29  

---

## 6. Key Concepts

Some stuff will stay in the log even tho its fixed  

---

## 7. Lessons Learned

The logs should be take care of for data leaks  

---

## 8. Credential (Password)
```
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```
