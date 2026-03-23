# Bandit Level 6 → Level 7

## 1. Objective

The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing I did was since I knew it was on the server used / find -group -user -size  
• Then I saw many denied permissions so I redirected the errors using 2>/dev/null  
• So I got the path and read it using cat  

---

## 4. Execution

Commands

```
Find -group -size -user  
2>/dev/null  
cat
```

Explanation  
Explain:  
• Since I already have the information I need I searched with them using find  
• 2>/dev/null is used to redirect errors to the specidied path usually /dev/null is used since its like a black hole  

---

## 5. Result

• Successfully retrieved the password for the next level  

---

## 6. Key Concepts

• Redirecting errors  

---

## 7. Lessons Learned

Sometimes due to errors you cant what you are looking for so redirecting them always is the best approach  

---

## 8. Credential (Password)

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```
