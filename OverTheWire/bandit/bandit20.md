# bandit 20
```
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think
```
This is an interesting problem. Here we have to start a server using `nc` and run `suconnect <portnumber>` with it, which is match the password and give us the next password.<br>
To setup the listening server, we will use the following command:
```bash
echo "<current_password>" | nc -l -p 1234 # or any port
``` 
This will give us an empty cursor in between the screen, on which if we type and enter anything, it will close the server. Now here comes the use of tmux, the terminal multiplexer. We have to run tmux and split into 2 panes, one side we will run the server and on the other side, we will run the `suconnect` command. 
<br>

```bash
tmux new -s base #base is name of session
```
The command to split the terminal into 2 panes is `Ctrl+b %` and to switch between panes, we can use `Ctrl+b <arrow_key>`. The command to run the server is:
```bash
echo "<current_password>" | nc -l -p 1234 # run in one pane
```
Now run the `suconnect` command in the other pane:
```bash
./suconnect 1234 # run in other pane
```
Now this will match the passwords, and we will get the next password in the pane where server is running. And we are done.