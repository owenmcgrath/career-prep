# Problem 5.5

## Problem statement

Explain what the following code does: ((n & (n-1)) == 0)

## Solution Attempt

This is checking to see if a value subtracted by 1 has the complete opposite bits.

101 -> 100 false

1->0 false
0 -> 100000... false

10 -> 01 true

100 -> 011 true

1000 -> 0111 true

It is checking to see if this value is an exponent of two! This is including zero which is the two's complement. 

### Listen

## Examples

## Brute Force

## Optimize

## Walk Through


## Implement

'''

'''

## Test


## Notes. 