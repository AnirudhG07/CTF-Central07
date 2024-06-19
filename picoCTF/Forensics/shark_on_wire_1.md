# shark on wire 1
This problem deals around with looking into all data packets that are being transferred between the client and the server. The data packets are stored in a file called `capture.pcap`. The file can be opened using Wireshark. 
<br>

Ill directly go to the solution-
<br>

If you check UDP packets, for the src='10.0.0.5' and dest='10.0.0.13', there are various packets and looking at them one by one, we see the data hex values spell 'picoCTF{N0t_a_flag}` or similar. While for dest='10.0.0.12', the data hex values spell 'picoCTF{StaT31355_...' which is the flag.
<br>

We have two options, either manually extract it(faster in my opinion) or use the python code below-
```python
from scapy.all import *
pcap = rdpcap('capture.pcap')
for p in pcap[UDP]:
    try: 
        if (p[IP].src=='10.0.0.2') and (p[IP].dst=='10.0.0.12'):
            print(p[Raw].load.decode('UTF-8'), end='')
    except:
        pass
```
This will give you the flag. And we are done.
<br>

**NOTE:**
1. You need to download scapy using `pip install scapy`
2. The dest may change between 12 or 13 in 10.0.0.12 for you.

### Flag
```
picoCTF{StaT31355_636f6e6e}
```