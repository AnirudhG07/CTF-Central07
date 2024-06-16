# natas6
You try few things - 
1. SQLi, like `' OR 1=1` or `admin'--`, none of these work. (I tried since word `Query` was written.)
2. You see the source code. You find `includes/secret.inc`. You put it in the website link as `.../includes/secrets.inc`, you get nothing.
3. An empty website is always sus. You check Source Code and you see the secret password!
```php
<?
$secret = "...";
?>
```
Now just put this secret in the original website and you get the password for the next level.