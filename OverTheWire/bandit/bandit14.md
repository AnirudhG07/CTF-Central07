# bandit 14
```
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
```
From the above, we can see that we have to submit the password of the current level to port 30000 on localhost. We can do this using the command -
```bash
echo "<password_current_level" | nc localhost 30000
```
And we are done.