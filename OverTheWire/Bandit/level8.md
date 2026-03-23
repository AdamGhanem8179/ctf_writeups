# Bandit Level 8 → Level 9

## 1. Objective

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once 

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was using cat data.txt | uniq -u  
• This made me find the hard way that I didn’t grasp the correct understanding of how it works with the result I got  
• So after researching I knew that I should sort it first since it only cancels the ones that are after each other  
• So I used sort data.txt | uniq -u  

---

## 4. Execution

Commands

```
Uniq -u  
cat  
|  
sort
```

Explanation  
Explain:  
• Uniq -u prints the lines that has a single occurrence (if they are after each other)  
• Sort is used to sort a file placing duplicates beside each others  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Some commands needs something prior to them to be executed correctly  

---

## 7. Lessons Learned

i believe this is the best lesson I learned till now which is I need to deeply understand the commands and how they work  

---

## 8. Credential (Password)

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
