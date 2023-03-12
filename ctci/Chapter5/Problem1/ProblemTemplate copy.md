# Problem 5.1

## Problem statement
Insertion: You are given two 32 bit numbers N and M and two bit positions i and j. Write a method to inert m into n such that m starts at bit j and ends  at bit i. You can assume bits j through i have enough space to fit all of m. 

i.e. if M = 10011 you can assume there are at least 5 bits between j and i. You would not for example have j = 3 and i = 2.  because m could not fully fit between bits 3 and bit 2

## Solution Attempt

### Listen

inserting M into N. M will start at bit j and end at bit i. 

can i assume that i & j are contained within m ? that is there will be no bit overflow?  yes.
can i assume bit i is less than bit j ? yes

## Examples
N = 1000000000, M = 10011, i=2, j=6
output N = 10001001100

## Brute Force

We could loop from i to j, clear the bits, then exclusive or n shifted to the left by i ? 

O(N) where N is the j - i. time O(1) space. 

## Optimize

The only optimization we could make here is avoiding the loop so that we are in O(1) time. 
Is it actually worth doing this? we only have to care about an order of 64 bits so it might be ok if its always less than 64. 
I think we should because realistically bit math applies to low level operations and generally low level operations get called a lot. 
i.e. graphics libraries.

We can't do bit shifts and then returns as we'll lose the data. 

It seems like we will have to loop!

After getting a hint, we can create a mask with bit shifting. 

## Walk Through

first check if i or j is bigger than the size of the integer. We'll use an unsigned long, so should be less than 64. 
set a mask to be a full unsigned long.
shift it to the right by (64 - j + i) bits.
shift it to the left by i bits. 
flip it. 
and it with the input.  

## Implement

'''
public ulong Insertion(ulong m, ulong n, int i, int j)
{
    if(i > 64 || j > 64) return ~0; //failed.
    ulong mask = ~((~0 >> (64 - j + i)) << i);
    return ((n & mask) | (m << i));
}

'''

## Test


## Notes. 
-needed hint to solve optimal
different from book solution but also right. 