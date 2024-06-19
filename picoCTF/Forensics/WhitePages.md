# WhitePages
This problem involves dealing with hex of the given `whitepages.txt` file and analyse the pattern occuring of `20` and `e28083`. The occurence of `20` is not equal and that is big clue of what should be done.
<br>

If we see the hex data, it looks like this-
```
0000000 80e2 e283 8380 80e2 e283 8380 e220 8380
0000010 e220 8380 80e2 e283 8380 80e2 e283 8380
0000020 e220 8380 80e2 2083 80e2 e283 8380 80e2
0000030 e283 8380 e220 8380 80e2 2083 80e2 2083
0000040 2020 80e2 e283 8380 80e2 e283 8380 80e2
0000050 2083 e220 8380 e220 8380 80e2 2083 80e2
0000060 2083 e220 8380 80e2 e283 8380 2020 80e2
0000070 2083 e220 8380 2020 2020 80e2 2083 80e2
0000080 e283 8380 80e2 e283 8380 2020 80e2 2083
0000090 80e2 2083 80e2 2083 80e2 e283 8380 80e2
00000a0 2083 80e2 e283 8380 80e2 2083 e220 8380
00000b0 80e2 e283 8380 80e2 e283 8380 e220 8380
. . .
```
We can see that `20` and `e28083` are repeating in a pattern. So here is a python code which gives us the binary of the hex data and then we can convert it to ascii.
```python
from pwn import *

with open('./whitepages.txt', 'rb') as f:
  data = f.read()

data = data.replace(bytes.fromhex('e28083'), b'0').replace(bytes.fromhex('20'), b'1')

data = data.decode('ascii')

print(unbits(data))
```
Here we convert spaces to 1's (i.e. `20`) and `e28083` to 0's. Then we convert the binary to ascii and we get the flag. And we are done.

### Flag
```
picoCTF{not_all_spaces_are_created_equal_3b6a8e2c}
```