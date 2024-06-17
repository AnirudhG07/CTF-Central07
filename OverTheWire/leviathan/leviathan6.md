# leviathan 6

When we open the leviathan6, we get a file called `leviathan6`, which wants an input of 4 digit number. If it is correct, then it will give us the shell to next level as usual, else it will output "Wrong". 
<br>
Now from ltrace function, we do not see any number being compared to so its hard to guess. Well then we will brute force it. Lets run the following loop in shell to input number from `0000` to `9999` by-

```bash
for i in {0000..9999}; do ./leviathan6 $i; done
```
This will output -

```bash
Wrong
Wrong
...
Wrong
$
```
Now we are done. Check `whoami` in the shell(we are `leviathan7`). Let's extract the password to the next level by-

```bash
cat /etc/leviathan_pass/leviathan7
```
And we are done!