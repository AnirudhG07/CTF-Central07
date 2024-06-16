# natas8
This one is straight up reverse ciphering. From the source code, we get the `submit` is what we input, which is passed through series of changes to finally get the hexadecimal `encodedSecret`.<br>
This we perform the below operations to `encodedSecret`.
1. Hex to Text (because of `bin2hex`)
2. Reverse it (because of `strrev`)
3. base64 decode (because of `bas64_encode`)
We get a text, which we input in the box, and you get the password for natas9!
