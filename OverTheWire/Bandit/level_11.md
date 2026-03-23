# Bandit Level 11 → Level 12

## 1. Objective
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

---

## 2. Environment
• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology
Step-by-step approach:  
• Since I knew it was ROT-13 I used the command cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

---

## 4. Execution

### Commands
    cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

### Explanation
Explain:  
• Since it is ROT-13 I rotated the letters using the tr which transforms them and using the ROT13 form 

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
`7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`
