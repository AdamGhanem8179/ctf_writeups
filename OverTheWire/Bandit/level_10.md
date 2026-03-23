# Bandit Level 10 → Level 11

## 1. Objective
The password for the next level is stored in the file data.txt, which contains base64 encoded data

---

## 2. Environment
• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology
Step-by-step approach:  
• It was a one step since I knew it was as base64 I just used cat data.txt | base64 -d

---

## 4. Execution

### Commands
    cat data.txt | base64 -d 

### Explanation
Explain:  
• Since I knew it was base64 I just gave the output of the file using cat and piping to the decoder of base64 where you just add -d  
________________________________________

---

## 5. Result
• Successfully retrieved the password for the next level  

---

## 6. Key Concepts
• If I know what is the coding I can decode it in a simple way ________________________________________

---

## 7. Lessons Learned
When encrypting I should avoid simple and easy encryption that can be decoded easily

---

## 8. Credential (Password)
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
