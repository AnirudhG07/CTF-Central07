## leviathan 1
You see a binary `check` file which you can run and input password to. But we do not know the password. So we can simply do-
```bash
ltrace ./check
```
This is used for getting signals and checks done at each step(in a concise way).
Here you see the password is compared to 'sex'. Thus we input password as 'sex' and we enter another shell.
<br>

When we try `whoami`, we see we are in `leviathan2`. Thus by the rule, we can access password to leviathan2 if we are in leviathan2. To get the password, simply run-
```bash
cat /etc/leviathan_pass/leviathan2
```
and we are done.