# rps-casino

Category-Cryptography

We're opening a new casino! The only game is rock-paper-scissors though...

## Solution
In the code given, it is mentioned that we need to win rock-paper-scissors against the computer 50 times in a row. For this, we are provided with 56 free trials. The entire challenge is based on LFSR(Linear Feedback Shift Register). To understand how it worked, I checked the video by [Computerphile](https://www.youtube.com/watch?v=Ks1pw1X22y4&t=463s) which gave an amazing explanation. 

`
 def LFSR():

state = bytes_to_long(os.urandom(8))

while 1: 

	yield state & 0xf

	for i in range(4):

		bit = (state ^ (state >> 1) ^ (state >> 3) ^ (state >> 4)) & 1

		state = (state >> 1) | (bit << 63) `
An LFSR is mainly used to generate pseudo-random numbers.
In the code, the variable state is an 8-byte long string generated using urandom and then converted to long, which is a long integer number. 
Then a for loop is called which runs from 0 to 3, where the variable state is XORed with itself but by shifting the LSBs first once, then thrice and then four times. At the end, the result obtained from this bitwise operation is ANDed with 1 to get the last digit. The state is then updated by shifting the RSB by 1 and then setting the value of MSB to the value of bit.
Basically the yield statement acts like the return statement itself, but instead of returning the values all at once, it returns them one by one. 
The value returned by calling the LFSR function keeps on changing after each win, loss or a tie. For the computer

**0 = Rock, 1 = Paper, 2 = Scissors**

The only region is I am a noob and can't get a code running to get a correlation between the randomly generated numbers and obtaining the LFSR values. If I could somehow get that to work, I would be able to predict the values which the computers would generate and get the flag
