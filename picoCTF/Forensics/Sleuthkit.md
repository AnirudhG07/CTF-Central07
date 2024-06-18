# Sleuthkit Intro
Run the below and you are done-
```bash
# decompress the gzip file
gzip disk.img.gz
# run mmls as instructed
mmls -a disk.img
```
Now you get output as -
```
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```
Run the netcat link and input `202752` and you get the flag.