# Bandit Level 7 → Level 8

## 1. Objective

The password for the next level is stored in the file data.txt next to the word millionth 

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was check if data.txt is present in the directory im at  
• Next I tried to read it but found out that there is a lot of lines  
• So I looked at the hint that the password is present beside millionth  
• So I used the command cat data.txt | grep millionth  

---

## 4. Execution

Commands

```
grep  
cat  
|
```

Explanation  
Explain:  
• Since I know what is present beside the password I used the cat to read the file and send the result to the grep which will search through the file and print the line that contains millionth  
• Piping takes the result of 1 and gives it to 2 example 1|2  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• mixing commands to reach the result  

---

## 7. Lessons Learned

Sometimes I might know a word or something beside my goal and that will save me a lot of time searching  

---

## 8. Credential (Password)

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
