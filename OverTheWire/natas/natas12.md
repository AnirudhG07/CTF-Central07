# natas12

When we read the code, we understand the following things-
1. Whatever filename we give, it is gonna change it to some random 10 letter string
2. It changes filetype to .jpg
3. It uploads the file and php automatically executes it, when you open the link. (Hence php is useful)

So we write a php code as `file.php`, with the following content-
```php
<?php
echo passthru('cat /etc/natas_webpass/natas13');
?>
```
This is supposed to give us the password. (Please search google on how to run a code of terminal using php)<br>
Now the main part. Since it converts it to jpg, we need to prevent that, else there is no use of execution. And Barpsuite is the best tool to do this.<br>
Open Barpsuite and in Proxy after you click Upload file, you see the new name of the file made as `some10letr.jpg`, just convert that to `.php` and you are done. This will show success upload file and when you click on the link, you get the password to the next level!