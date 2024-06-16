# natas9

This one is good. From the source code given, we can see it is operating a terminal command, and the first that comes to mind is the use of `;`. So we try `hello; ls`. And very well it gives output as `dictionary.txt`. <br>

But the problem is that you try around various possibilities of ls, but it wont get us the password. One thing left is to try extracting password like `; cat /etc/natas_webpass/natas10`. This gives us the password and we are done. This is sort of unintuitive, but these are how you exploit such vulnerabilities. Sometimes they are designed to let you pass these.
