# Problem 4.9

## Problem statement

BST Sequences A BST was created by traversing through an array from left to right and inserting each element. Given a 
binary search tree with distinct elements, print all possible arrays that could have led to this tree.

## Solution Attempt

### Listen

Can the BST have duplicate entries? no.

## Examples

    2
1       3 prints {2 1 3}, {2, 3, 1}

## Brute Force

Essentially need to print every possible root to leaf traversal pattern. 
we could throw into a nested list of values for each node in the tree. 
then iterating through that list build all possible combinations of characters from the previous list of strings. 

O(n) O(2^n) to build the string list.

Also O(2^n) space. 

## Optimize

## Walk Through


## Implement

'''

'''

## Test


## Notes. 