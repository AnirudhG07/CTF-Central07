# Special
This is one of those CTF's where our command input is messed with and we have to figure out some symbolic expression which will do the job for us.

## Solution
If you try any english simple commands, their first letter will become Capital and useless. Commands are usually not beginning with capital letters. 
<br>Now if we try `.*`, `/?/?`, etc. they are filtered again or get autocorrected for english as mentioned in problem statement.
<br>

From `symbols.md` list in this repo's Terminal tricks directory, there is something which works like magic.<br>
This is-
```bash
## Command(left side) # Output(right side)
${var?ls}	# var: ls
${:ls}	# Bad substitution
${var=ls}	blargh
${var=cat blargh}	# cat: blargh: Is a directory
${var=cd blargh}	# ${var=cd blargh}
${var=ls blargh}	# flag.txt
${var=cat blargh/flag.txt}	# This gave the flag
```
These are various combinations you try which works. You get the flag with this. 