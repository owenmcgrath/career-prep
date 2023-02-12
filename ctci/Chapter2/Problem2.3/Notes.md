# Problem 2.3

## Problem statement
Delete Middle Node. Implement an algorithm to delete a node in the middle of a singly linked last, given only that node
The middle is not necessarily the exact middle.

## Solution Attempt

### Listen

can you assume that the inputted node is not first or last? yes.

## Examples

{a,b,c,d,e,f} Delete C -> {a,b,d,e,f}

## Brute Force
set the current node to the next node, delete the last node.
This is done in O(n) time and O(1) space

Since the linked list is singly linked, we have no way to find out what is before the provided node. 

## Optimize

if allowed, we could set the node to be a "ref" and set the reference to be next. is this ok? no
then we should use two pointers. one that holds the previous node, and one that holds an iterative node. 
copy the next value to the current value
once we reach the end set prev.Next to null

## Walk Through
initialize node it, and prev
while it.Next isn't null
    it.Value = it.Next.Value
    prev = it
    toDelete = toDelete.Next

## Implement

'''
void DeleteMiddleNode(ref LinkedListNode toDelete)
{
    LinkedListNode prev = null;
    LinkedListNode it = toDelete;
    while(it.Next != null)
    {
        it.Value = it.Next.Value;
        prev = it;
        it = it.Next;
    }
    prev.Next = null;
}

'''

## Test

{a,b,c,d,e,f}
{a,b,d,d,e,f}
{a,b,d,e,e,f}
{a,b,d,e,e,f}
{a,b,d,e,f,f}
{a,b,d,e,f}


## Notes. 