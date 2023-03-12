# Problem 5.6

## Problem statement

Write a function to determine the number of bits you would need to flip to convert integer A to integer B.

## Solution Attempt

### Listen

## Examples

11101 01111 -> 2
101 010 -> 3

## Brute Force

A brute force method would be to loop through each bit of A and B to check if they are equal or not. 

## Optimize

Rather than looping through both a marginal improvement would be to take the exclusive or and count the set bits. 

We could use Brian Kernighan's algorithm to get the number of set bits in logarithmic time on the xor. 

## Walk Through


## Implement

'''
int numSetBits(int n)
{
    int count = 0;
    while(n)
    {
        n = n & (n - 1)
        count++;
    }
    return count;
}

int Conversion()
{
    return numSetBits(a ^ b);
}

'''

## Test


## Notes. 