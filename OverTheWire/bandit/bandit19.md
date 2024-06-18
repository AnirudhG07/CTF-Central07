# bandit 19
```
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
```
The setuid binary is `bandit20-do`. When we run it without any arguments, it gives us the following output:
```bash
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```
This means we can run any command as `bandit20` user. So we can run `cat /etc/bandit_pass/bandit20` to get the password.
```bash
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
```
And we are done.