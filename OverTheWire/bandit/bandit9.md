# bandit 9
The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, beginning with several `=` characters. Let's find the password.
We will run the below command to find the password and understand it.

```bash
strings data.txt | grep "=="
```
* The `strings` command prints the human-readable strings in the data.txt file. Else it will output - `grep: data.txt: binary file matches` not the password.
* grep `==` filters out the lines that contain `==` in the output of the strings command.

We get the output as -

```bash
*N========== the
========== password
========== is
w========== FGUW5ilL...qeY # password hidden purposely
```
And we get the password! And we are done.