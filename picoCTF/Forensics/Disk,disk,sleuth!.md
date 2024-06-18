# Disk, disk, sleuth!
This is also easy. Download the disk image and run the following -
```bash
gzip -d dds1-alpine.flag.img.gz
srch_strings -a dds1-alpine.flag.img | grep "picoCTF"
```
And we are done.

### Flag
```
picoCTF{f0r3ns1c4t0r_n30phyt3_a011c142}
```

