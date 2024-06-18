# bandit 17
```
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19
```
This is a simple `diff` problem. We can use `diff` to compare the two files and get the password. The command is:
```bash
diff passwords.old passwords.new
```
This has the output of format-
```bash
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< znK19XRJuZTd8BvCEVW4NQjtNJbdFLNC
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```
Since passwords.new is 2nd argument, the text to be chosen is the second one as the password. <br>
When you logout and login as bandit18 with above password you get "Byebye!" message. This is normal and it will happen.
And we are done.
**NOTE:** You can't normally login to bandit18, you have to provide the command to run with the login command to perform any actions. See bandit18.md for solution.