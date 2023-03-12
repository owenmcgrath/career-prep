# Problem 5.3

## Problem statement

Flip Bit to Win. You have an integer and you can flip exactly one bit from a 0 to a 1. Write code to find the length of the longest sequence of ones you could create. 

## Solution Attempt

### Listen

## Examples

11011101111 -> 8
100011110 -> 5

## Brute Force

an O(n^2) solution would be to look for zero bits, then count all chained 1 bits checking for a maximum. 

## Optimize

This can be done O(n). 

Keep a maximum to output. 
Keep two variables. old (the last finished chain) current (the chain currently being counted)

Check the LSB. 
If its one increment current
if its 0? 
    max current+old+1 to the existing max. 
    set current to old

return max.

## Walk Through


## Implement

'''
int FlipBitToWin(int input)
{
    if(~input == 0) return 32;
    int max;
    int old;
    int curr;
    for(int i = 0; i < 32; i++)
    {
        if(((input >> i) & 1) == 1)
        {
            curr++;
        }
        maximum = Math.Max(maximum, curr + old + 1);
        if((input >> i) & 0 == 0)
        {
            old = curr;
            current = 0;
        }
    }

    return max;
}

'''

## Test


## Notes. 

use while loops instead of for loops modifying the input on bit math questions. 
Less iterations and magic numbers.