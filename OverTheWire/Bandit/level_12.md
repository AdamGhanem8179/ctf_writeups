# Bandit Level 12 → Level 13

## 1. Objective
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

---

## 2. Environment
• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology
Step-by-step approach:  
• This exercise was about using file checking what is it (gz bz2 tar xxd)  
• Then decompressing/decoding it  

---

## 4. Execution

### Commands
    file
    xxd -r 
    bzip -d
    gzip -d
    tar -xf 
    gzip -d

### Explanation
Explain:  
• File is used to check what the file is made of so if itws  gzip for example I use gzip -d (d means decompress and -r revert)________________________________________

---

## 5. Result
• Successfully retrieved the password for the next level  

---

## 6. Key Concepts
• Breaking complex problems into layers________________________________________

---

## 7. Lessons Learned
I would say the lesson I learned is trusting the evidence I got using file and how temp is useful to bypass permission issues

---

## 8. Credential (Password)
`FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`
