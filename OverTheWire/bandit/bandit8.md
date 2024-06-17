# bandit 8
The password for the next level is stored in the file `data.txt` and according to the website, and is the only line of text that occurs only once
Let's find the password. 
<br>
We will use two new commands for our purpose. Lets run the below command to find the password and understand it.

```bash
sort data.txt | uniq -u
```
* You can use the `sort` and `uniq` commands to find the line of text that occurs only once in the data.txt file. 
* `sort data.txt` sorts the lines in the data.txt file.
* `|` pipes the output of the sort command to the uniq command.
* `uniq -u` filters out the lines that are repeated in the output of the sort command, leaving only the lines that occur once.

The `uniq -u` command will return the line of text that occurs only *once* in the `data.txt` file. This is the password for Bandit Level 9. And we are done!
