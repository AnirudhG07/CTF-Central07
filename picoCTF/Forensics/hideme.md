# hideme
When you download it, `flag.png` file will be made. If you run -
```bash
strings flag.png
```
You will see there is a `secret/` written in the text. Thus we can extract the file using-
```bash
binwalk -e flag.png
``` 
This will give us extracted file directory.<br>
Inside this we have `secret/` directory, inside which is `flag.png`. When you open the image, you see the image right away. And we are done.

### FLAg
```
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_d55982e8}
```