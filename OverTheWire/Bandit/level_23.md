# Bandit Level 23 → Level 24

## 1. Objective

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!
NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

---

## 2. Environment

• Platform: OverTheWire (Bandit)  
• Access Method: SSH  
• Tools Used: Linux (ubuntu)

---

## 3. Methodology

Step-by-step approach:  
• First thing i did was enter /etc/cron.d/ then use ls to see whats inside  
• Since I need to reach level 24 I used cat on the file containing 24  
• Then I got how it works and cat /usr/bin/cronjob_bandit24.sh  
• After that I entered tmp since I cant create a file in the home directory (I don’t have permission) and created a file  
• Then I copied my file and moved it to the /var/spool/bandit24/foo/  
• Then I waited a minute and read the file with cat  

---

## 4. Execution

Commands
```
cd /tmp
echo "cat /etc/bandit_pass/bandit24 > /tmp/pass24" > script.sh
chmod +x script.sh
cp script.sh /var/spool/bandit24/foo/
cat /tmp/pass24
```

Explanation  
Explain:  
• I entered tmp since I cant create files in any other place  
• Chmod +x file is used to make the file executable  
• Then I used cp and not mv since if I used mv cron will execute it then delete it so I wont get the password back  

---

## 5. Result

• Got the password for level 24  

---

## 6. Key Concepts

understanding how cron deeply works and permission bypass  

---

## 7. Lessons Learned

An attacker doesn’t need permission rather he needs an executable location  

---

## 8. Credential (Password)
```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```
