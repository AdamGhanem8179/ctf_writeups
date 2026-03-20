# Bandit Level 0 → Level 1

## 1. Objective

Find the password inside the `readme` file.

---

## 2. Environment

* Platform: OverTheWire (Bandit)
* Access Method: SSH
* Tools Used: Linux (Ubuntu)

---

## 3. Methodology

Step-by-step approach:

* First, I checked what files are present using `ls`
* Then I read the file using `cat`

---

## 4. Execution

### Commands

```bash
ls
cat readme
```

### Explanation

* `ls` is used to list the files in the directory
* `cat` is used to read the content of a file
* I didn’t use `ls -a` since I already knew the file wasn’t hidden
* I expected to find the file directly and read its contents

---

## 5. Result

* Successfully retrieved the password for the next level

---

## 6. Key Concepts

* Listing directory contents using `ls`
* Reading file content using `cat`
* Basic interaction with files in Linux

---

## 7. Lessons Learned

Even though these commands are simple, they are fundamental. Most tasks in Linux start with listing files and checking their contents, so being comfortable with these basics is important.

---

## 8. Credential (Password)

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```
