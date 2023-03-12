# Problem 5.4

## Problem statement

Next Number: Given a positive integer print the next smallest and the next largest number that have the same number of 1 bits in their binary representation.

## Solution Attempt

### Listen

## Examples

000 -> FALSE no next largest or smallest
001 -> FALSE, no next smallest
(int.MaxValue) -> FALSE no next largest.

010 -> large: 100, Small 001

110110 -> large: 111100, Small 110101

11111 -> large: 111110, small: FALSE no next smallest

1101 -> large: 1110, small: 1011


## Brute Force

starting from the value, we could guess and check by incrementing and counting the 1s, then decrementing and counting the 1s. 
This starts to be in a O(n^2) kind of category. 

## Optimize

There is a pattern here. It appears that moving the right most 1, to the next right most slot with a 0 gives you the lowest number
moving the right most 1 to the closest left slot gives you the next highest number. 

This means we can solve this in O(n) time. 

## Walk Through

if its 0, 1 or the maximum integer return false. 

if its all 1s without leading zeros return false. (if n+1 & n == 0) 

find the first 0 index.
find the first 1 index.

if 1 is to the left of 0
    set 1 to 0 and 0 to 1, print next smallest.
    find the next 0 to the left of 1
        set that idx to 1 and the 1 index to 0, print largest 
if 1 is to the right of 0
    set 1 to 0 and 0 to 1 print next largest. 
    find the next 1 to the left of 0
        set that idx to 0 and this index to 1. print smallest.

## Implement

'''
int SetBit(int val, int idx, bool bit)
{
    return val | ((bit ? 1 : 0)<< idx);
}

int FindNext(int val, int startIdx, bool bit)
{
    val >>= startIdx;
    int toCompare = bit ? 1 : 0;
    int idx = startIdx;
    while(val != 0)
    {
        idx++;
        if(val & toCompare == toCompare)
        {
            return idx;
        }
        val >>= 1;
    }

    return idx;
}

bool NextNumber(int value)
{
    if(value == 0 || value == 1 || value == int.MaxValue) reutrn false;
    if((n+1 & n) == 0) return false;

    int firstZero = FindNext(value, 0, false);
    int firstOne = FindNext(value, 0, true);

    if(firstOne > firstZero)
    {
        Console.WriteLine("Next Smallest: " + SetBit(SetBit(value, firstOne, false), firstZero, true));
        int newZero = FindNext(value, firstOne, false);
        Console.WriteLine("Next Largest: " + SetBit(SetBit(value, firstOne, false), newZero, true));
    }
    else 
    {
        Console.WriteLine("Next Largest: " + SetBit(SetBit(value, firstOne, false), firstZero, true));
        int newOne = FindNext(value, firstZero, true);
        Console.WriteLine("Next Smallest: " + SetBit(SetBit(value, newOne, false), firstZero, true));
    }

    return true;
}

'''

## Test


## Notes. 