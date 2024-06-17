# bandit7
This level again is based on using `find` command. The properties of the file is mentioned by the website which is are -

1. Owned by user `bandit7`
2. Owned by group `bandit6`
3. 33 bytes in size

The command to find the file is -

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Lets understand this command-
* `/` specifies the root directory.
* `-user bandit7` specifies that the file must be owned by user `bandit7`.
* `-group bandit6` specifies that the file must be owned by group `bandit6`.
* `-size 33c` specifies that the file must be 33 bytes in size. The c stands for bytes.
* `2>/dev/null` is used to suppress the error messages.

This gives me the file `/var/lib/dpkg/info/bandit7.password`. Now I can read the content of the file using the `cat` command. Run the command -

```bash
cat /var/lib/dpkg/info/bandit7.password
```
And we are done.