# Disk, disk, sleuth! II
This one the tool to use is not specified, but we need to find some tool which can help us do it. First we do-
```bash
binwalk -e dds2-alpine.flag.img
```
Inside the xtracted directory, we have `ext-root` folder, inside which we have lots folders like `usr`, `root`, `bin`, etc. If we find the `down-at-the-bottom.txt` file, we find it in root folder. Inside it we have the file which contains the flag.
```bash
_______________________________________________________________________________________
   1   │    _     _     _     _     _     _     _     _     _     _     _     _     _
   2   │   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \
   3   │  ( p ) ( i ) ( c ) ( o ) ( C ) ( T ) ( F ) ( { ) ( f ) ( 0 ) ( r ) ( 3 ) ( n )
   4   │   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/
   5   │    _     _     _     _     _     _     _     _     _     _     _     _     _
   6   │   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \
   7   │  ( s ) ( 1 ) ( c ) ( 4 ) ( t ) ( 0 ) ( r ) ( _ ) ( n ) ( 0 ) ( v ) ( 1 ) ( c )
   8   │   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/
   9   │    _     _     _     _     _     _     _     _     _     _     _
  10   │   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \   / \
  11   │  ( 3 ) ( _ ) ( 0 ) ( b ) ( a ) ( 8 ) ( d ) ( 0 ) ( 2 ) ( d ) ( } )
  12   │   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/   \_/
_______________________________________________________________________________________
```
We get the flag. If we want to use sleuthkit, we can use-

```bash
fls -r -o 2048 -p dds2-alpine.flag.img | grep "down-at-the-bottom.txt"
```
And we find the location of the file. And we are done.

### Flag
```
picoCTF{f0r3ns1c4t0r_n0v1c3_0ba8d02d}
```