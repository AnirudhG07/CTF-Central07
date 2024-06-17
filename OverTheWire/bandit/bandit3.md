# bandit 4
The goal is to find the password for the next level. The password is stored in a file named `inhere` located in the home directory.
<br>

We enter the shell and see the files using `ls`. We see a directory named `inhere`. We enter the directory using `cd inhere` and see the files using `ls`. But we don't see anything. In such cases we uses `ll` or `ls -la` to see hidden files. We see a file called `...Hiding-From-You`. To get the password we can use the below commands -

```bash
cat ...Hiding-From-You
cat .*
```
And we are done.