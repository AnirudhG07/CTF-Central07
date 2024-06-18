# bandit 21
```
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
```
This level is now even making us use crontab usages, but it is simply looking here and there.<br>
As instructed, we peek into `/etc/cron.d/` and find a file named `cronjob_bandit22`. We read the file using `cat` and find the command being executed is `cat /etc/bandit_pass/bandit22`.
```bash
# output is
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
This shows we need to see whats the the shell script. Using `cat /usr/bin/cronjob_bandit22.sh` we get- 
```bash
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
Since we do not have the permission to see `/etc/bandit_pass`, we will see the contents of the file `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv` which is the password for the next level.
```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
And we are done.
