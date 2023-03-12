# Problem 5.7

## Problem statement

Pairwise Swap: Write a program to swap odd and evven bits in an integer with as few instructions as possible (e.g. 0 and 1 swap, 2 and 3 swap)

## Solution Attempt

### Listen

## Examples

1010 -> 0101
1111 -> 1111
0000 -> 0000

## Brute Force

iterating by two from 0 to the full integer you could do a get on each bit then a set on each bit. 

## Optimize

2 gets and 2 sets for every 2 bits. 

What if we were to check if the pair matches, then we wouldnt need to do a swap? 
For a 01 bit we could add by a value

1 -> 2
0100 4 -> 1000 8 add 4. 
0111 7 -> 1011 11 add 4. 
1000 8 -> 0100 4 subtract 4
1011 11 -> 0111 7 subtract 4. 

So if the bit is 01, add 1 << pair iteration * 2
if the bit is 10 subtract 1 << pair iteration * 2

## Walk Through

set a count variable
while input >> count is not 0
    if val >> count & 3 is 3 or val >> count ^ 3 == 0 
        continue
    if val >> count & 2 == 2
        add 1 << count
    if val >> count & 1 == 1
        subtract 1 << count
return val
    

## Implement

'''
int PairwiseSwap(int value)
{
    int count = 0;
    int toCheck = value;
    while(toCheck != 0)
    {
        if(toCheck & 2 == 2)
        {
            value += (1 << count);
        }
        else if(toCheck & 1 == 1)
        {
            value -= (1 << count);
        }

        toCheck >>= 2;
        count += 2;
    }
    return value;
}
'''

## Test


## Notes. 

not optimal. 

mask the odd bits and shift them to the right by 1.  (0xaaaaaaaaaaa)
mask the even bits then shift them to the left by 1 (0x555555555555)
OR those two together