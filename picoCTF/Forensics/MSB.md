# MSB

This is an amazing problem showing us how to extract the MSB from the image and get the flag. There are a couple of ways of doing this, one using stegsolve software and one using command line. I will be showing the command line one.
<br>
The description and name of challenge suggests data may be hidden in the Most Significant Bit (MSB) of the RGB pixels values within the image.<br>
There exists a python script called `sigBits.py` that can be used to extract the MSB from the image.-

```bash
wget https://artifacts.picoctf.net/c/306/Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png

pip install Pillow
wget https://raw.githubusercontent.com/Pulho/sigBits/master/sigBits.py

python3 sigBits.py -t=msb Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png
```
This creates a file called `outputSB.txt` which contains the flag.
```bash
cat outputSB.txt | grep "picoCTF{"
```
And we are done

### Flag
```
picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_3a219174}
```