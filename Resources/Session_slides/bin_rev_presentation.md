---

title: Databased CTF-Quest
author: Anirudh Gupta, Aditya Arsh & Databased team
sub_title: Binary Files, Exploitation and Reverse Engineering

---

## Last time  

Last time we dealt with Ciphers and learnt how to decipher some common
ciphers, how to use online tools and did some online CTF's.
<!-- pause -->

## Today  

We will we be going into binary files, how to extract flags out of them,
and also a bit on reverse engineering.
<!-- pause -->
For all this, the use of terminal is very important so let's first get
to understand some basics of it.

<!-- end_slide -->

## Terminal  
The following are some basic Terminal commands that we should know.

<!-- pause -->
# Directory motion
- cd - for entering a directory 
<!-- pause -->
- ls - for listing out sub files & directory
<!-- pause -->
- ls -la or ll - above plus hidden files
<!-- pause -->
- pwd - absolute address of your location
<!-- pause -->

# Making and removing file
<!-- pause -->
- rm - remove file
<!-- pause -->
- rmdir - remove empty directory
<!-- pause -->
- rm -rf - remove permanently any directory or file
<!-- pause -->
- mkdir - make a directory
<!-- pause -->
- touch - make a file
<!-- pause -->

# Text editors
- vim or neovim(nvim)
<!-- pause -->
- nano
<!-- pause -->

# General Commands
- echo - print something in terminal
<!-- pause -->
- echo "something" > filename.filetype - appends it
<!-- pause -->
- chmod +x `filename` - for making a file executable
<!-- pause -->
- ./*filename* - to run that executable file
<!-- pause -->
- cat - view file in terminal
<!-- pause -->
- bat - better cat
<!-- pause -->
- wget - download file from a link
<!-- pause -->
- mv - move things(cut), which also renames
<!-- pause -->
- grep - finds text in directory
<!-- pause -->
- clear -clears screen
<!-- pause -->
- man or tldr - description of command, always helps
<!-- pause -->

Now we are set to understand how to deal with some binary files
and understand how to work with them.

<!-- end_slide -->

## What we will do today ->
We will hopefully (based on time) look at the following topics-

<!-- pause -->
# Dealing with binary files
<!-- pause -->
# Software Application
<!-- pause -->
- Ghidra (or you may use IDA Pro)
<!-- pause -->
- Jadx
<!-- pause -->
- Wireshark, etc.
# Debugger GDB, python debugger
<!-- pause -->
and problem's in between and at the end.

<!-- end_slide -->

 # Dealing with Binary files ->
When you do `$ cat <binary_file>`, you get to see if its binary.
<!-- pause -->

When you open it, it's total gibberish and non sense. You may see
some english test but that may or may not make any sense.
<!-- pause -->

So here are few commands you should know in order to make sense 
out of what is going on around and in the file.

<!-- end_slide -->

 # Some commands for binary files  

Try to run these in order. Always best to follow your fav order.
<!-- pause -->
# Commands are:
<!-- pause -->
- file
<!-- pause -->
- exiftool
<!-- pause -->
- strings *filename* | less
<!-- pause -->
- strings *filename* | grep `'{'`
<!-- pause -->
- hexdump or hexedit or hexcurse
<!-- pause -->
- objdump -d *filename*
<!-- pause -->

<!-- end_slide -->

### Download time
Before we move on to examples and problems, I hope everyone has the following commands and softwares available-
<!-- pause -->
1) exiftool, file, strings
```bash
sudo apt install <command> # for linux
brew install <command> # for macOS
```
For windows, go to Google, search for it and download.
<!-- pause -->
2) Ghidra, Jadx(optional)
```bash
`brew install ghidra` # for macOS
```
For linux and windows, you can download from net. (I never tried)
<!-- pause -->
3) gdb or lldb
```bash
sudo apt install gdb # for linux
sudo port install gdb # for MacOS
brew install lldb # for MacOS as wellp
# ggdb (gdb) may cause errors so lldb
```
<!-- end_slide -->
## Example 1  

Let's deal with our first example, a file called `example1`.
<!-- pause -->

This is about basics tool usage of binary files.
<!-- pause -->
I hope you found the flag!

<!-- end_slide --> 

## Problem 1  

Go to the repository of CTF-Quest and solve problem 1. Flag format is `dtbdCTF{...}`.
<!-- pause -->
`A program has been provided to you, what happens if you try to run it on the command line?`

<!-- pause -->
```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->

## Hint: 
```bash
chmod +x example1
./example <what argument should you write?>
```

<!-- end_slide --> 

### Solution Problem 1
1) Decrypt whatever you got
<!-- pause -->
2) When you run `strings example1`, notice you will find the same base64 cipher. Just give it a
hit and trial and who knows that might be the flag. 
<!-- pause -->

# Flag is
```markdown
dtbdCTF{cipher_usages}
```
<!-- end_slide --> 

## Example 2

Here we will do some find some vulnerabilities of a C program file, and find the flag.
This is also something important we should all know.
<!-- pause -->

Please see example2.c file from the repository. 
<!-- end_slide --> 

## Example 3 - GNU Debugger GDB

GNU Debugger 
<!-- pause -->
# Commands
- b or breakpoint
<!-- pause -->
- r or run
<!-- pause -->
- next (for code line) `number`
<!-- pause -->
- nexti (for assembly code) `number`
<!-- pause -->
- step (for stepping into a function)
<!-- pause -->
- c or continue
<!-- pause -->
- help (important because you will forget these)
<!-- pause -->


<!-- pause -->
Now we will see this simple example-
<!-- pause -->

# Problem statement
<!-- pause -->
`Can you figure out what is in the eax register at the end of the main function?`

Report flag in the format `dbdCTF{...}`

<!-- end_slide --> 

## Problem 2

Go to the repository of CTF-Quest and solve problem 2. 
<!-- pause -->
# Problem statement
```markdown
`main` calls a function that multiplies `eax` by
a constant. The flag for this challenge is that
constant in decimal base. If the constant you find
is `0x1000`, then flag will be `dbdCTF{4096}`.
```
<!-- pause -->

```bash +exec
for i in $(seq 15 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->

# Hint:
Keep a record of how rax is changing. What is relation between rax and eax? 

<!-- end_slide --> 

### Solution Problem 2
The solution is simple. We see a call happening at *(main +38).
Then we note the the values before the function and after the function.
We use the following commands-
<!-- pause -->
```bash
chmod +x problem2
gdb ./problem2
layout reg
layout next # for my fav layout
b *(main + 38)
r # run the code till breakpoint
c # Note: eax value is 0x28e or 654
nexti # eax value becomes 8439870
```
<!-- pause -->
Now we simply divide `8439870` with `654` to get `12905`.
<!-- pause -->
# Flag is
```markdown
dbdCTF{12905} 
```
<!-- end_slide --> 

## Problem 3
<!-- pause -->
Let's do another problem! This one is easy!

<!-- pause -->
# Problem Statement
<!-- pause -->

Find the Flag. Format is `dbdCTF{...}`.
<!-- pause -->

```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done

```
<!-- pause -->

# Hints:
```
Just observe your hexeditted file closely!
```
<!-- end_slide -->
### Solution 3
<!-- pause -->

Look closely to your hexedit file. That's the solution! It's hidden like
`...C...T...F...{...`
<!-- pause -->

# Flag is
<!-- pause -->
```markdown
dbdCTF{6df215eb3cc734070267031a15b0ab36c}
```
<!-- end_slide -->


## Example 4  
<!-- pause -->

Let's do some debugging now of a python file. Let's solve *example4.py*.

_Note:_ flag format is *dtbdCTF{...}*

<!-- end_slide -->

## Problem 4
<!-- pause -->
Now let's do a problem. This will be based on a minor bug in the code.
You would need to apply some common sense on how you can get to the answer.
<!-- pause -->
_Note:_ No hints for this.
<!-- pause -->

```bash +exec
for i in $(seq 10 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- end_slide -->
### Solution problem 4
<!-- pause -->

Well, you just needed to print the big strings.
You get the password as: `happychance`
<!-- pause -->


Then you see `i = -1` in `arg122` function doesn't make sense. So by intuition, you
have to change to `i = 0`. And you get the flag!
<!-- pause -->
# Final answer: 
```bash
dbdCTF{c30bfu5c4710n_f7w_b8062eec}
```
<!-- pause -->

You need not to `pdb` though. Those who did well, look closely if it is actually needed and then move on!

<!-- end_slide --> 

## Example 5  

Now let's do an example with ghidra. I hope everyone now has Ghidra installed.
<!-- pause -->
# Problem Statement
`What is the flag post 0x70?`
<!-- pause -->

_Note:_ flag format is *dbdCTF{...}*

<!-- end_slide -->

## Problem 5

Let's use some skills we learned to apply to another problem which we will need to use Ghidra for.
<!-- pause -->
Please open problem5 from the repository. And try to figure it the flag.
No particular problem statement. Just find the flag of format `dtbdCTF{...}`
<!-- pause -->
```bash +exec
for i in $(seq 15 0)
do # TIMER
    echo  "$i minutes left"
    sleep 60
done
```
<!-- pause -->
# Hint:
```markdown
Don't go overboard and move here and there.
Find a big list of functions, go over each of them.
```

<!-- end_slide -->

### Solution 5
<!-- pause -->
This problem might be hard, but once figured out, it shoudn't take much time.
Once you reach a function called `FUN_0010298a`, you see a big list of functions.
<!-- pause -->

```java

void FUN_0010298a(void)

{
  ada__calendar__delays__delay_for(1000000000000000);
  FUN_001023a6();
  FUN_001026e6();
  FUN_0010233e();
  FUN_001023a6();
  FUN_00102852();
  FUN_00102886();
  FUN_001028ba();
  FUN_00102922();
  FUN_001023a6();
  FUN_00102136();
  FUN_00102206();
  FUN_0010230a();
    ...
    ...
    ...

  return;
}
```
Go over each of them, see the first argument, each has some corresponding text. Well that's it!
<!-- pause -->
# Flag:
```markdown
dtbdCTF{d15a5m_ftw_eab78e4}
```

<!-- end_slide -->


## Example 6 

This one is adopted from `picoCTF`. We will basically see where and how to use JADX. 
You can download it later on. 

<!-- pause -->
# `Why do we need jadx?`
JADX is crucial in CTFs for decompiling Android APKs and Java binaries, revealing their underlying code for analysis. It helps participants understand obfuscated code, identify vulnerabilities, and automate analysis tasks. By simplifying reverse engineering processes, JADX aids in debugging, testing exploits, and honing crucial cybersecurity skills. 
<!-- pause -->

_Note:_ 
 <!-- pause -->
- You can't edit in jadx-gui
- Searching is really easy, better than Ghidra. 
- It's better to see a binary in jadx first, just for the sake of searching. If the file is supported great!

<!-- end_slide -->
### That's it

<!-- pause -->
```markdown
Thank you everyone for attending this CTF session.
Any Questions?
```
<!-- pause -->
## Summary
<!-- pause -->
# Terminal basics
<!-- pause -->

# Binary file tools
<!-- pause -->

# Vulnerability
<!-- pause -->

# GNU Debugger 
<!-- pause -->

# PDB 
<!-- pause -->

# Ghidra 
<!-- pause -->

# JADX
<!-- pause -->

.\
.\
.\
.\
.\
.\
.\
.\
.
### - DATABASED CTF-QUEST

