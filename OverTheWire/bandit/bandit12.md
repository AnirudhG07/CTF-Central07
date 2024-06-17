# bandit 12

The password for the next level is stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed. Let's find the password.<br>
According to the website, the file is compressed multiple times. So we can uncompress it using `gzip`, `bzip`, etc. Since we do not have the permission to operate in home directory, lets create a temporary directory using the command -
```bash
mktemp -d
```
This will create a folder `/tmp/tmp.4m01w5a1U1` where `4m01w5a1U1` is a random string(different for you). We can use this folder to store the compressed files and uncompress them.
<br>

Let's copy `data.txt` to the temporary directory and navigate to it.
```bash
cp data.txt /tmp/tmp.4m01w5a1U1/hex_data
```
This will create `hex_data` which contains the data from `data.txt`. When we look at the file's hexdump, the initial few hex's show the file type. 

## Analysis
We can use the command `xxd` to get the hexdump of the file and its binary representation(in Ascii).
```bash
xxd hex_data # hexdump
xxd -r hex_data # binary as text
```
We see the data of format-
```bash
bandit12@bandit:/tmp/tmp.yOEVSZw2Gb$ xxd -r comp1.gz
=Rnfdata2.binB��BZh91AY&SYK����lf�?���������������������߰0� =@��@��z��M4
@�M���4                                                                     �4h�@z�Q�h�����t�
Wkö���;>d%K��x��=���0xP�2���X��m:���t׀��8��l��|$�ZА�PL�Q���4���W�<�H��R�S�B_�Г�g�$=0�~n���&U��W��4b�����
                      �%��q=Y�: @�,�Tw#2G�!`7�ˆU;���֩K�9m��!Pm3%�7��[-5m�N�F`�C.�%��~
;���Q�ڤ�v��Q4Q��*����Ip������fB���͋��$���X�YH����j�?���TL����P�r�@\�[��$�p�� �Zc�Gmx0��Α�"}���r�%x�rE8P�K��,qB
```
This is the compressed version and we have to uncompress it to get our data back.
<br>
Let's put the binary data in some other file.
```bash
xxd -r hex_data > comp1.gz
```

## Compression 1 - gzip
For gzip compressed files the header is `\x1F\x8B\x08`. Looking at the first line, we see that these are the first bytes of the file.
```bash
bandit12@bandit:/tmp/tmp.4m01w5a1U1$ cat comp1.gz
00000000: 1f8b 0808 3d52 6e66 0203 6461 7461 322e  ....=Rnf..data2.
```
Thus this is a gzip compressed comp1.gz. We can decompress it using the command -
```bash
gzip -d comp1.gz
```
This creates the file `comp1` which is the decompressed version of `comp1.gz`. We can see our file is still not in readable format, it must still be compressed.

## Compression 2 - bzip2
For bzip2 compressed files the header is `\x42\x5A\x68`. Let's check the header of the file.
```bash
bandit12@bandit:/tmp/tmp.yOEVSZw2Gb$ xxd comp1
00000000: 425a 6839 3141 5926 5359 054b 81c9 0000  BZh91AY&SY.K....
```
Thus this is a bzip2 compressed file. Let's transfer the file to `comp2.bz2` using-
```bash
mv comp1 comp2.bz2
```
We can decompress it using the command -
```bash
bzip2 -d comp2.bz2
```
We get another unreadable file `comp2`. Let's check the header of this file using `xxd comp2`. We notice is is again compressed with `gzip` since `1f8b 0808` is present in header.

## Compression 3 - gzip
Let's perform the below steps just as compression 1-
```bash
mv comp2 comp3.gz # renaming
gzip -d comp3.gz # decompress
xxd comp3 # check header
```
This still doesn't look readable but much better.

## Compression 4 - tar
The file contains the header as-
```
00000000: 6461 7461 352e 6269 6e00 0000 0000 0000  data5.bin.......
00000010: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000020: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000030: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000040: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000050: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000060: 0000 0000 3030 3030 3634 3400 3030 3030  ....0000644.0000
00000070: 3030 3000 3030 3030 3030 3000 3030 3030  000.0000000.0000
00000080: 3030 3234 3030 3000 3134 3633 3334 3531  0024000.14633451
00000090: 3037 3500 3031 3132 3530 0020 3000 0000  075.011250. 0...
```
This shows its an archive file. We can extract it as `tar` using the command -
```bash
mv comp3 comp4.tar
tar -xvf comp4.tar
```
This will extract the file `data5.bin` which is the password for the next level.

## Compression 5 - tar
The data5.bin is similar to `tar` format and we can extract it using the command -
```bash
tar -xv data5.bin
```
This gives us `data6.bin` whose header tells us it is a `bzip2` compressed file.
## Compression 6 - bzip2
We can decompress the obtained file using the command -
```bash
mv data6.bin comp5.bz2
bzip2 -d comp5.bz2
```
This gives `comp5` which is again a `tar` file.

## Compression 7 - tar
We can extract the file using the command -
```bash
tar -xf comp5
```
This gives us `data8.bin` which is a `gzip` compressed file.

## Compression 8 - gzip
We can decompress the file using the command -
```bash
mv data8.bin comp6.gz
gzip -d comp6.gz
```
This gives us `comp6` which is FINALLY the password for the next level.
<br>
We can run the command `cat comp6` to get the password.<br>
And we are done.