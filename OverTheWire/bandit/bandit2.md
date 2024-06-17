# bandit 2
The goal is to find the password for the next level. The password is stored in a file named `spaces in this filename` located in the home directory.
<br>
Now, if you try - 

```bash
cat spaces in this filename
```
This won't work as you can't use the cat command directly because of the spaces in the filename, it will end up running `cat spaces`. So, you need to use cat like -

```bash
cat spaces\ in\ this\ filename # OR
cat "spaces in this filename" # OR
cat * # for Lazy people
```
And you get the password. And we are done.