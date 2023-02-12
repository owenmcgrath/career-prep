# Problem 2.7

## Problem statement

Given two singly linked lists determine if the two lists intersect, return the intersecting node. 

## Solution Attempt

### Listen

- What are the values of the linked list? integer
- Handle empty lists? no

## Examples

4, 1
      >  8, 4, 5 returns node 8
5,6,1

1,9,1
        > 2,4 returns node 2
3

2,6,4 > return null

1,5
## Brute Force

The brute force way would be to do a 2D iteration through each linked list, and check if the node is equal ,then return true.
This is O(n^2) time and O(1) space

## Optimize

What if we were able to iterate backwards through each linked list? We could try to see if theres a match that way.
The problem is reversing list A would break list B.

What if we calculated the length of list B. Then reversed list A. We could then check if the length of list b changed. This won't work as we won't be able to check if list b changed without using memory

If we used O(n) space we could push the elements on both lists onto two stacks then pop each off of each stack comparing them until theres 
a mismatch, then returning.

Theres a way to do this in place. If we attach the end of linked list a to the end of linked list b, then we can loop through both ensuring that they match 

## Walk Through

initialize iterators itA and itB.
Loop through each list while the nodes are not equal, if a is null set to bhead. if b is null set to b head

## Implement

'''
LinkedListNode<int> Intersection(LinkedListNode<int> aHead, LinkedListNode<int> bHead)
{
    LinkedListNode<int> aIt = aHead;
    LinkedListNode<int> bIt = bHead;

    while(aIt != bIt)
    {
        aIt = aIt == null ? bHead : aIt.Next;
        bIt = bIt == null ? aHead : bIt.Next;
    }

    return aIt;
}
'''

## Test


## Notes. 
- Got hint from leetcode for inplace solution.
- combining lists helps here.