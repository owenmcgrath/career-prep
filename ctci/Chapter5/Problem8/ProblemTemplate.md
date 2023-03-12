# Problem 5.8

## Problem statement

Draw Line: A monochrome screen is stored as a single array of bytes, allowing eight conescutive pixels to be stored in one byte. 
The screen has width w where w is divisible by 8 (that is no byte will be split across two rows.) The height of the screen of course 
can be derived from the length of the array and the width. 

## Solution Attempt

### Listen

How is the byte array formatted? if the width is 16 for example are the first two bytes index 0 and 1 in the array? 
yes. 

## Examples

00000000, 00000000
00000000, 00000000, w = 2, x1 = 3, x2 = 15, y = 0

result
0011111, 11111111
0000000, 00000000

## Brute Force

first validate. check if row is less than 0 or too big. Check if x is less than 0 or greater than max width. 

write a helper function to generate a mask. shift ~0 to the right (smallIndex + 8 - largeIndex), then to the left (8-largeIndex)

find the first index of the row (y * w)
bool reachedLeft
bool reachedRight
loop from 0 to w
    left = reachedLeft ? 0 : 8;
    right = 8
    if !reachedLeft && x1 > idx * 8 and less than idx(+1)*8
        left = x1 - idx*1 + 8
        reachedLeft = true
    if x2 > idx * 8 and less than idx + 1 * 8
        right = 8 - (x2 - idx*8)
        reachedRight = true;
    screen[y*w + idx] = [y*w + idx] & mask(left,right)
    if(reachedRight) return;

## Optimize

## Walk Through


## Implement

'''
bool DrawLine(int width, int x1, int x2, int y, ref byte[] screen)
{
    if(y < 0 || y*w > screen.Length - 1 || x1 < 0 || x2 < 0 || x1 > width*8 - 1 || x2 > width*8 - 1) return false;
    bool reachedRight, reachedLeft;
    int left,right;
    for(int i = 0; i < w; i++)
    {
        left = reachedLeft ? 0 : 8;
        right = 8;
        if(!reachedLeft && x1 > i*8 && x1 < (i+1)*8)
        {
            left = x1 - (i*8);
            reachedLeft = true;
        }
        if(x2 > i*8 && x2 < (i+1) * 8)
        {
            right = 8 - (x2 - i*8)
            reachedRight = true;
        }
        screen[y*w + i] = screen[y*w + i] & LineMask(left,right);
    }

}

byte LineMask(byte left, byte right)
{
    return ((byte)0xFF >> (left + (8-right))) << right;
}

'''

## Test


## Notes. 