## leviathan 1
You see a binary `level3` file which you can run and input password to. But we do not know the password. So we can simply do-
```bash
ltrace ./level3
```
Here you see the password is compared to 'snlprintf'. Thus we input password as 'snlprintf' and we enter another shell.
<br>

When we try `whoami`, we see we are in `leviathan4`. Thus by the rule, we can access password to leviathan4 if we are in leviathan4. To get the password, simply run-
```bash
cat /etc/leviathan_pass/leviathan4
```
and we are done.