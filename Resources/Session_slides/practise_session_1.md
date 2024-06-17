---

title: Databased CTF-Quest
author: Anirudh Gupta, Aditya Arsh & Databased team
sub_title: Practise session

---

## Last time
We did some Web Exploitation like SQLi, digging around, Proxy Interception, cookies, etc.
<!--pause -->
## Today
<!--pause -->
We will do some practise!!!
<!-- end_slide-->

### Terminal based problems
Terminal based problems involves various tricks and tips you should know about shell scripting and features of bash. 
<!--pause -->
## Problem 1 - Special
<!--pause -->
This problem is an example which I will solve, let's get into it!
<!--pause -->
If you try any english simple commands, their first letter will become Capital and useless. Commands are usually not beginning with capital letters. 
<!--pause -->
Now if we try `.*`, `/?/?`, etc. they are filtered again or get autocorrected for english as mentioned in problem statement.
<!--pause -->
From `symbols.md` list in this repo's Terminal tricks directory, there is something which works like magic. This is-
<!--pause -->
```bash
## Command(left side) # Output(right side)
${var?ls} # var: ls
${:ls} # Bad substitution
${var=ls} # blargh
${var=cat blargh} # cat: blargh: Is a directory
${var=cd blargh} # ${var=cd blargh}
${var=ls blargh} # flag.txt
${var=cat blargh/flag.txt} # This gave the flag
```
<!--pause -->
These are various combinations you try which works. You get the flag with this. 
<!-- end_slide-->
## Problem 2 - Specialer
You guys will solve this problem. You have 10 minutes time. Time starts now.
<!-- pause -->

```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->

# Hint
<!--pause -->
Think about keyboard shortcuts(in built) which you use instead of just typing commands.

<!-- end_slide-->
### Solution
<!-- pause -->
SSH into the problem using `ssh -p <port> ctf-player@saturn.picoctf.net` and password `<password>`, which will be given.
<!--pause -->
The most helpful tool here in this problem according to me is the TAB button functionality which automatically prints out the contents in a directory which can be applied on for a command.
<!--pause -->
Thus, when you open a terminal and simply press TAB, you get a list of command you have, which shows you that you can use "echo", "pwd" , "printf" and "cd" and thats all you need.
<!--pause -->
- When you try `cd TAB`, then you see list of directories.
<!--pause -->
- When you try `printf TAB`, then you get a list of files present.
<!--pause -->
- When you try `echo $(<file.txt)`, you get the contents of the flag.
<!--pause -->
Now traverse each folder `abra`, `ala`, `sim` and echo contents of each file as mentioned above. 
<!--pause -->
You get the answer in `ala/kazam.txt`. 
<!-- end_slide-->

## Problem 3 - flag-shop
Again you guys will solve this problem. This is based on `C`ommon sense. You have 10 min, time starts now.
<!-- pause -->

```bash +exec
for i in $(seq 15 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!--pause -->
# Hint
Think about properties of integers in C and how they can be exploited.
<!-- end_slide-->

### Solution 
<!-- pause--> 
Download the `Source` code - `store.c` mentioned in the problem and check it out. We make the below observations which we will be used in the solution(other observations may not be required)-
<!--pause -->
1. Initial balance = 1100
<!--pause -->
2. We need to make money > 100000, then we can obtain the flag. 
<!--pause -->
3. We can buy 900$ flags, but we cannot input a negative number. 
<!--pause -->
4. Our code only checks if number of input flags>0 for 900$ case
<!--pause -->

Now run the netcat link to open our flag-shop. We get various options as expected. From our understanding of code and the fact code is in "C language", we can use the concept of overflow i.e. a very huge number wraps around and becomes negative or positive(depends on number).
<!--pause -->
Now we can simply input a suitable number which will become negative and using the maths of code (i.e. balance = original - cost), since cost becomes negative, our balance will increase.
<!--pause -->
Now we perform the following tasks-
<!--pause -->
```
Number of flags = 12345678
```
<!--pause -->
This gives us enough money to buy the flag!

<!-- end_slide-->
## Problem 4
<!--pause -->
Refer the link to problem link from OverTheWire Leviathan. I will show you leviathan0, 1 and 2. You all will solve leviathan3 to 6. 
<!--pause -->
# Levithan 0
<!--pause -->
See the contents in the home directory using `ll` command. You see their is `/.backup/bookmarks.html`. You can simply grep for "leviathan1" using-
<!--pause -->
```bash
grep -r "leviathan1" .
```
<!--pause -->
And you get the text-
<!--pause -->
```bash
./bookmarks.html:<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html |
This will be fixed later, the password for leviathan1 is <password>"
ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```
<!--pause -->
And we are done.
<!-- end_slide-->
## leviathan 1
<!--pause -->
You see a binary `check` file which you can run and input password to. But we do not know the password. So we can simply do-
<!--pause -->
```bash
ltrace ./check
```
<!--pause -->
This is used for getting signals and checks done at each step(in a concise way).
<!--pause -->
Here you see the password is compared to 'sex'. Thus we input password as 'sex' and we enter another shell.
<!--pause -->
When we try `whoami`, we see we are in `leviathan2`. Thus by the rule, we can access password to leviathan2 if we are in leviathan2. To get the password, simply run-
<!--pause -->
```bash
cat /etc/leviathan_pass/leviathan2
```
<!--pause -->
and we are done.
<!-- end_slide-->
## leviathan2
<!--pause -->
Here we see a `printfile` binary function which takes input of a file and displays that. But it doesnt display all the files. Although we have access to `/bin/cat` so we can see that.
<!--pause -->
Now to get the flag at `/etc/leviathan_pass/leviathan3`, we need a way to create symlink to that file so that it can be accessed, direct access is not possible (after testing out) using-
<!--pause -->
```bash
./printfile /etc/leviathan_pass/leviathan3
```
<!--pause -->
Now we create a temporary directory where we will do our work using -
<!--pause -->
```bash
mktemp -d
```
<!--pause -->
This will create a folder in `/tmp/tmp.mOUs8tRl2T` or some code. We give all file permissions for convenience using-
<!--pause -->
```bash
chmod 777 /tmp/tmp.mOUs8tRl2T
```
<!--pause -->
Let's understand the printfile file more deeply. When we input 2 files, it only prints the output for the first file argument and ignores the second. We can use this for our benifit. The printfile binary function is likely designed to prevent reading certain files, possibly by checking the filename against a list of disallowed paths or patterns.
<!--pause -->
Let's make some preperations. Create a symlink file to our target file by -
<!--pause -->
```bash
ln -s /etc/leviathan_pass/leviathan3 /tmp/tmp.mOUs8tRl2T/'symlink file'
```
<!--pause -->
In this example, printfile might only see `/tmp/tmp.mOUs8tRl2T/symlink` when it checks the filename, and since that doesn't match any disallowed patterns, it will proceed to open the file, following the link to `/etc/leviathan_pass/leviathan3`.
 
<!--pause -->
This is a common type of security vulnerability known as a path traversal vulnerability, where an application allows access to files it shouldn't by failing to properly validate or sanitize file paths.
<!-- end_slide -->
### Your turn
<!-- pause -->
Solve problems after `leviathan2`. You have 30 min in all. I will be discussing solved problems in between as well, so that you can move on if you can't solve a particular one.
<!-- pause -->
```bash +exec
for i in $(seq 30 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- end_slide-->
### Problem 5
<!-- pause -->
## Web Exploitation 
<!--pause -->
We will do some problems on natas based on the time we have left. In the last session, we did till natas3. But now you can do upto natas10. So let's get started. If you have any doubts, let me know, we will solve that problem.