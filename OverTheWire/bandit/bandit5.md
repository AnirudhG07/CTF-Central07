# bandit 5
The goal is to find the password for the next level. The password is stored in a file somewhere in the `inhere` directory and has the following properties as given on the website:

1. human-readable
2. 1033 bytes in size
3. not executable

Now let's analyse the folders. Inside `inhere` we have `maybehere00` to `maybehere19` folders, inside which we have files with names `regular_english` or `-dashed_ones`. We need to find a way to display everything and then filter out the password. If we try-
```bash
for i in {00..19}; do cd maybehere$i; cat ./*; echo "\n"; cd ..; done
```
We see tons of text popping up which we cant handle nor figure out the password. But one thing we can guess is that we need a file whose contents are small and do not contain non-english gibberish. So, we can use the `find` command to find the file that matches the given properties. Run the command -
```bash
find . -type f -readable -size 1033c ! -executable
```
Lets understand this command- 
* `.`  specifies the current directory.
* `-type f` specifies that we're looking for files.
* `-readable` specifies that the file must be readable.
* `-size 1033c` specifies that the file must be 1033 bytes in size. The c stands for bytes.
* `! -executable` specifies that the file must not be executable.
* The `find` command will return the path to the file that matches the given properties.

This gives me the file `./maybehere07/.file2`. Now I can read the content of the file using the `cat` command. Run the command -
```bash
cat ./maybehere07/.file2
```
And we are done.