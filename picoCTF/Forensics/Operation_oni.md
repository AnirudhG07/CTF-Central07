# Operation Oni
Let's get into it. We will look at 2 solutions for this.
Before that we will download and gunzip the image file-
```bash
gzip -d disk.img.gz
```

## Solution 1 - Using Autopsy
Launch Autopsy (see some youtube video if you don't know how to use it). Open the image file and try finding something related to "keys" or "ssh" or "flag", etc. We find that their is `.ssh/` in the `/root` directory, inside which we have a file `id_ed25519` which contains the key to ssh. 
<br>
Let's copy the key to a file-

```bash
touch key_file
# copy paste the key using vim
```
Now run the ssh as mentioned in the question-
```bash
ssh -i key_file -p 56255 ctf-player@saturn.picoctf.net
```
This will give us an unprotected key error which we can fix by changing the permissions of the key file-
```bash
chmod 600 key_file
```
Run the command and we safely enter the server. Now we have `flag.txt` waiting for us-
```bash
cat flag.txt
```
And we are done.

## Solution 2 - Using binwalk
We can use binwalk to extract the files from the image. First we need to install binwalk-
```bash
sudo apt-get install binwalk
```
Now we can extract the files from the image-
```bash
binwalk -e disk.img
```
Now we can see the extracted files in the `_disk.img.extracted/` directory. We can see the `.ssh/` directory in the `/root` directory. We can see the `id_ed25519` file which contains the key to ssh.
<br>
Now it follows as before.
