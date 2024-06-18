# bandit 15
```markdown
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…
```
This level is similar to the previous one. We have to submit the password of the current level to port 30001 on localhost using SSL encryption. We can do this using the command -
```bash
echo "<password_current_level" | openssl s_client -connect localhost:30001 -ign_eof
```
We get the password at the bottom and we are done.