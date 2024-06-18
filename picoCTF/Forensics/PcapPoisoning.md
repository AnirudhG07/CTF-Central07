# PcapPoisoning
Here if you try binwalk, file, exiftool, etc. you wont find anything useful. But if we try to find picoCTF in the strings, we get the flag.
```bash
strings trace.pcap | grep "picoCTF"
```
And we are done.

### Flag
```
picoCTF{P64P_4N4L7S1S_SU55355FUL_4624a8b6}
```