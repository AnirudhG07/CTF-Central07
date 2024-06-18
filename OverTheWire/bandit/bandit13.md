# bandit 13
```
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on.
```
From the above, after logging in, we see that we have a file called `sshkey.private`. We can use this key to login to the next level. Let's go to the localhost of bandit4 using the RSA key given us by-
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```
This will log us into the next level. Now we can read the password for the next level using the command -
```bash
cat /etc/bandit_pass/bandit14
```
This will give us the password for the next level. And we are done.