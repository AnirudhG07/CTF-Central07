# Redaction gone wrong
This is an easy problem. You can directly select the last redaction and it will show you the text. DONE!

## OR
If you are unable to do it, you need to tool called `pdftotext` which you can download by-
```bash
brew install poppler
# or any other package manager, see on net
```
Now use-
```
pdftotext Financial_Report_for_ABC_Labs.pdf
```
This will give another file called `Financial_Report_for_ABC_Labs.txt`. Open it and you will get the flag.

### Flag
```
picoCTF{C4n_Y0u_S33_m3_fully}
```