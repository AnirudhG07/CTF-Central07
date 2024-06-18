# Secrets of the Polygot

We can open the pdf to see the the end portion of the flag which is `1n_pn9_&_pdf_724b1287}`. Now we need to somehow get the first part of the flag.
<br>
If we try-
```bash
binwalk -e flag2of2-final.pdf
```
and analyse, we wont get anything.
<br>
But if we convert things to png, we get the first part of the flag.
```
mv flag2of2-final.pdf flag2of2-final.png
```
Now if we open the png file, we get the first part of the flag.
```
picoCTF{f1u3n7_
```
And we are done.

### Flag
```
picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}
```
