# bandit 22
``` 
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.
```
This is the same as the one before. Let's go through this as before -
```bash
ls /etc/cron.d/
cat /etc/cron.d/cronjob_bandit23
```
We get the output as - 
```
@reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
```
Now let's see the contents of the shell script using `cat /usr/bin/cronjob_bandit23.sh` -
```bash
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
If we run this, it will copy the password of the current user to `/tmp/<md5sum>`. We can see the password by running `cat /tmp/<md5sum>` which is same as what we have.
<br>

So what we can do it run the shell script line by line ourself but with `whoami=bandit23` and then run the `cat /tmp/<md5sum>` to get the password.
```bash
whoami=bandit23
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
cat /etc/bandit_pass/$myname > /tmp/$mytarget
cat /tmp/$mytarget
```
And we are done.
