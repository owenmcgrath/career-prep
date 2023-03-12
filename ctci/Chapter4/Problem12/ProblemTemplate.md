# Problem 4.12

## Problem statement

You are given a binary tree in which each node contains an integer value. Design an algorithm to count the number of paths that sum to a given value. PAth doesnt need to start or end at the root or a leaf but must go downwards.

## Solution Attempt

### Listen
null tree? yes

## Examples

## Brute Force

We probably want to do a post order traversal here. Where we find the left most value and the right most value. Add to our current sum and check if its equal to the value.



## Optimize

## Walk Through

if this is null return
check if sum + current is equal to the value, if so increment path counter. 
add current to the sum.
recurse to the left
recurse to the right
subtract the current from the sum

this only works in the case that everypath goes through the root. which isnt true.

if this is null return
recurse to the left
recurse to the right.  
## Implement

'''

'''

## Test


## Notes. 