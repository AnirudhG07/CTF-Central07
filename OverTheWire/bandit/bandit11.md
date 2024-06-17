# bandit 11
The password for the next level is stored in the file `data.txt`, which is simply Caeser ciphered. We can get a hint that it matches with output of bandit10 as `The password is ...`. 
<br>
Using the above knowledge, we hit and try to see the shift is 13. We can use the `tr` command to decrypt the data. 

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
* The `tr` command translates the characters in the data.txt file.
* `'A-Za-z' 'N-ZA-Mn-za-m'` shifts the characters by 13 places in the output of the cat command.

And we are done.
