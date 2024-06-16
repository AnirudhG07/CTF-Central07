## leviathan 0
See the contents in the home directory using `ll` command. You see their is `/.backup/bookmarks.html`. You can simply grep for "leviathan1" using-
```bash
grep -r "leviathan1" .
```
And you get the text-
```bash
./bookmarks.html:<DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is <password>" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```
And we are done.