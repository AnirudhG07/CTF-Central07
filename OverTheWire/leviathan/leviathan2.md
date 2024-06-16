## leviathan2
Here we see a `printfile` binary function which takes input of a file and displays that. But it doesnt display all the files. Although we have access to `/bin/cat` so we can see that. Now to get the flag at `/etc/leviathan_pass/leviathan3`, we need a way to create symlink to that file so that it can be accessed, direct access is not possible (after testing out) using-
```bash
./printfile /etc/leviathan_pass/leviathan3
```
Now we create a temporary directory where we will do our work using -
```bash
mktemp -d
```
This will create a folder in `/tmp/tmp.mOUs8tRl2T` or some code. We give all file permissions for convenience using-
```bash
chmod 777 /tmp/tmp.mOUs8tRl2T
```
Let's understand the printfile file more deeply. When we input 2 files, it only prints the output for the first file argument and ignores the second. We can use this for our benifit. The printfile binary function is likely designed to prevent reading certain files, possibly by checking the filename against a list of disallowed paths or patterns.
<br>

Let's make some preperations. Create a symlink file to our target file by -
```bash
ln -s /etc/leviathan_pass/leviathan3 /tmp/tmp.mOUs8tRl2T/'symlink file'
```
In this example, printfile might only see `/tmp/tmp.mOUs8tRl2T/symlink` when it checks the filename, and since that doesn't match any disallowed patterns, it will proceed to open the file, following the link to `/etc/leviathan_pass/leviathan3`.
<br>

This is a common type of security vulnerability known as a path traversal vulnerability, where an application allows access to files it shouldn't by failing to properly validate or sanitize file paths.
