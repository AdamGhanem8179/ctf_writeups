# Bandit Level 30 → Level 31

## 1. Objective

There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was exactly the same as the previous level  
• Then when I found there is no point of it I tried to  check the tags  

---

## 4. Execution

Commands
```
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
cat README.md
git tag
git show secret
```

---

## 5. Result

• Got the password for level 31  

---

## 6. Key Concepts

Git is a huge database  

---

## 7. Lessons Learned

I should explore everything  

---

## 8. Credential (Password)
```
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```
