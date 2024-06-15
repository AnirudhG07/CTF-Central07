# dont-you-love-banners
This is a problem where we need to get permission to `flag.txt` using symlink concept and general terminal commands. 

## Solution
You get a link where _"crucial information"_ is hidden, you can netcat it - `nc tethys.picoctf.net <port1>`. There you see the password is leaked which is `My_Passw@rd_@1234`. <br>
Now you launch the other server which asks you the following question-
<br>

1. what is the password?
**Ans-** My_Passw@rd_@1234
2. What is the top cyber security conference in the world?
**Ans-** DEFCON 
3. the first hacker ever was known for phreaking(making free phone calls), who was it?
**Ans-** John Draper

You can simply search the bottom 2 question on net to get the answers of, to enter into the terminal of our attacking machine. 
<br>

From the problem statement, we traverse into `/root` directory, so let's go using `cd /root`. There we have 2 files- `flag.txt` and `script.py`, which is exactly the one when our link is run. But we do not have the permission to open flag.txt, but `script.py` does. That's the key, so we use script.py to open flag.txt. We can do this by symlinking `banner`->`flag.txt` so that it opens our flag instead of the banner message.
<br>

This banner is present in the `/home/ctf-player` directory. Thus we use the below to complete our task-
```bash
cd # STEP 1, go to home
rm banner # remove banner, else symlink wont work
ln -s ../../root/flag.txt banner
```
Now we are set to go. We simply exit and restart our the netcat server on the same port. And we get our flag displayed!!!

## Cheating skills
If we get password and port to some other user who has completed this task, we can run that to get the flag! LOL!