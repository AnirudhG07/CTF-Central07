# bandit 16
```
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
```
This is a simple port scanning problem. We can use `nmap` to scan the ports in the given range. The command is:
```bash
nmap -sV localhost -p 31000-32000
```
This will scan the ports in the range 31000 to 32000 on localhost. The output will show the ports that are open and the services running on them. We can see-
```bash
bandit16@bandit:~$ nmap -sV localhost -p 31000-32000

Starting Nmap 7.40 ( https://nmap.org ) at 2021-06-12 16:17 CEST
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00026s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE     VERSION
31046/tcp open  echo
31518/tcp open  ssl/echo
31691/tcp open  echo
31790/tcp open  ssl/unknown
31960/tcp open  echo

Nmap done: 1 IP address (1 host up) scanned in 0.08 seconds
```
We can use `openssl` to connect to the service and send the password to get the next password. The command is:
```bash
for i in {31046,31518,31691,31790,31960};do echo <password_bandit16> | openssl s_client -connect localhost:$i -ign_eof; done 
```
From this we see "Correct!" on port 31790(which makes sense since service was unknown). We take the RSA key from port 31970 and save it in a file. We can then use this key to connect to the service on port 31790 and get the next password. The commands are:
```bash
mktemp -d
# run below in the temporary directory
touch my.key # copy the RSA key in this file manually using vim
chmod 600 my.key # you cannot have 777 permission, it will give "too open" error
ssh -i my.key bandit17@localhost -p 2220
```
Now you are logged in as bandit17. You can get the password by running

```bash
cat /etc/bandit_pass/bandit17
```
And we are done.
