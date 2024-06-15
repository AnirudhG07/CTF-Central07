# Specialer
Specialer is a picoCTF General Skills problem. It involves directory traversal without using commands like `ls`, `cat`, etc. which is very frequently needed. Sometimes these problems are always helpful in a way we develop skills to use bash shell without the use of common commands.

## Solution
SSH into the problem using `ssh -p <port> ctf-player@saturn.picoctf.net` and password `<password>`, which will be given.

The most helpful tool here in this problem according to me is the TAB button functionality which automatically prints out the contents in a directory which can be applied on for a command.<br>Thus, when you open a terminal and simply press TAB, you get a list of command you have, which shows you that you can use "echo", "pwd" , "printf" and "cd" and thats all you need.
<br>

- When you try `cd TAB`, then you see list of directories.
- When you try `printf TAB`, then you get a list of files present.
- When you try `echo $(<file.txt)`, you get the contents of the flag.

Now traverse each folder `abra`, `ala`, `sim` and echo contents of each file as mentioned above. 
You get the answer in `ala/kazam.txt`. 
