# bandit 18
```
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
```
Now if you try log in using password obtained, it will show a `"Byebye!"` annoying message. So we have to provide the command to run with the login command to perform any actions. The command is:
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```
This will output the content of readme which is the password for next level. And we are done.