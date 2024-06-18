# Sleuthkit Apprentice
This solution doesnt involve usage of any sleuthkit tool, but rather `binwalk`. We need to extract the image file and try to find the file containing the flag.
```bash
binwalk -e disk.flag.img
cd _disk.flag.img.extracted/
```
Now we get look for the file name containing flag using-
```bash
find . -type f -name "*flag*"
./ext-root-0/root/my_folder/flag.uni.txt
```
We can hexedit this file to see-
```bash
hexedit ./ext-root-0/root/my_folder/flag.uni.txt
```
```bash
# OUTPUT
00000000   00 70 00 69  00 63 00 6F  00 43 00 54  00 46 00 7B  00 62 00 79  00 37 00 33  00 5F 00 35  00 75 00 72  .p.i.c.o.C.T.F.{.b.y.7.3._.5.u.r
00000020   00 66 00 33  00 72 00 5F  00 33 00 34  00 39 00 37  00 61 00 65  00 36 00 62  00 7D 00 0A               .f.3.r._.3.4.9.7.a.e.6.b.}..
```
This is the flag. We can write the flag on our own and we are done.

### Flag
```
picoCTF{by73_5urf3r_3497ae6b}
```