# natas11

For cipher lovers, this one is a bonus. Here we are given with a source code which explains how the encryption is done. We see `array( "showpassword"=>"no", "bgcolor"=>"#ffffff");` present and we must change no to yes.
<br>Notice the cookies, you have `data` having some text written, according to the source code, that cookie is basically the above array but in encryption. So our task is to find the key of XOR, and use it to decode the above array again, but with a yes.
<br>

**CORE CONCEPT:** let A, B, C be 3 texts such that `A XOR B = C`, then `B XOR C = A`, `C XOR A = B`. This is the vulnerability of XOR.
<br>
We follow the below steps- 
1. Convert the above to json(since the code uses json_decode)
We get `{"showpassword":"no","bgcolor":"#ffffff"}` (UTF-8)
2. We decode base64 for the cookie data ( which has %3D or something at the end).
3. We XOR that with the above json, to get the key. (You can use Cyber Chef)
Notice that the key is repeating, well good for you. Just extract that common part and use it.

4. Put XOR key as the 4 letter common part and above json with "yes". (UTF-8)
5. We take the new text and base64 encode it.
6. We get a big cookie text which is very similar to our original cookie.
7. We input this to the cookie as the new cookie, refresh.

And we have the new password. This was indeed tough to understand the code, since we may not be familiar with PHP.