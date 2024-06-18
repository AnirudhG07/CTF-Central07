# Mob Psycho
To extract contents in this `.apk` file, we can do-
```bash
binwalk -e mobpsycho.apk
```
This will create a directory called `_mobpsycho.apk.extracted/`. If we try grepping for the flag, we wont get anything. Neither do we have a hint what might be the file name. So we can try guessing the file name. If we try-
```bash
cd _mobpsycho.apk.extracted/
find . name="*.txt"
```
We get the location of the file at `./res/color/flag.txt`. Now we can see the flag which is in hex format. We can convert it to ascii using some online tool.
```
7069636f4354467b6178386d433052553676655f4e5838356c346178386d436c5f61336562356163327d
```
And we are done.

## Flag
```
picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_a3eb5ac2}
```