# bandit 1
The goal is to find the password for the next level. The password is stored in a file named `-` located in the home directory.
<br>
Now, if you try - 

```bash 
cat -
cat *
```
This won't work as you can't use the cat command directly because `-` is a special character that represents the standard input in Unix-like systems. So, you need to specify the full path of the file. 

```bash
cat ./- # OR
cat ./*
```
And you get the password. And we are done.