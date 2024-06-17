# leviathan 5

When we open the leviathan6, we get a file called `leviathan5`. We see the below results when we open using ltrace-
```bash
leviathan5@gibson:~$ ltrace ./leviathan5
__libc_start_main(0x804910d, 1, 0xffffd454, 0 <unfinished ...>
fopen("/tmp/file.log", "r")                                                                                   = 0
puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
)                                                                             = 26
exit(-1 <no return ...>
+++ exited (status 255) +++
```
Notice it uses `fopen`, this function returns a FILE pointer. If the file is successfully opened, the function returns a pointer to the file and if the file cannot be opened (due to any reason like file not found, or it is opened in write mode but we don't have write permission, etc.), it returns NULL.
<br>

Hence we can create a symlink in the name of `/tmp/file.log` to the password of the next level as-
```bash
ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
```
And now when we run `./leviathan5`, we get the password!