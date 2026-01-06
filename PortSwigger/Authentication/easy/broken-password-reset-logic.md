#Password Rest Broken Logic
Category : Web
Difficulty : Apprentice

#problem Summary
I need to reset the password of carlos and log in to his account and im given my credentials
wiener:peter
victims username : carlos

#initial thoughts
i noticed that i can easily check my email and to reset my password all what i need is my email 
and i initially thought that it is something related to the request so i should check it and using just an email is the most suspicious

#Exploration
first of all i tried to change just the name in the email from weiner to carlos then the same token and it failed then i tried to walk throught he process to check everything while checking the Requests on devtools
the name change didnt work since it generates a token for each user 

#Solution
after analyzing the Requests i found out that i can remove the tokenafter the reset so using Burp suite i removed all the tokens and changed the name from weiner to carlos 
because it doesnt validate the token anymore it trusts the username  and since all i need ot login o the account is the username (given) and the password i reseted iw as able to enter easily 

#Fix
After submission the token must exist
and the server mustd erive the username from the token
one time use only so replay wont work 
