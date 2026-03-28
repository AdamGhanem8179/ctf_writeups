# Bandit Level 31 → Level 32

## 1. Objective

there is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. The password for the user bandit31-git is the same as for the user bandit31.

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was exactly the same as the previous level  
• Then I followed the readme with the info I got and pushed  

---

## 4. Execution

Commands
```
git clone ssh://bandit31-git@bandit.labs.overthewire.org
:2220/home/bandit31-git/repo
cat README.md
echo "May I come in?" > key.txt
git add -f key.txt
git config --global user.name "bandit"
git config --global user.email bandit@overthewire.org
git commit -m "add key"
git push origin master
```

---

## 5. Result

• Got the password for level 32  

---

## 6. Key Concepts

How to work with git  

---

## 7. Lessons Learned

How to work with git pushing a file  

---

## 8. Credential (Password)
```
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```
