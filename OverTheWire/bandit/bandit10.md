# bandit 10
The password for the next level is stored in the file `data.txt`, which contains base64 encoded data. Let's find the password.
We will run the below command to find the password and understand it.

```bash
cat data.txt | base64 -d
```
* The `cat` command prints the content of the data.txt file.
* `base64 -d` decodes the base64 encoded data in the output of the cat command.

And we are done.