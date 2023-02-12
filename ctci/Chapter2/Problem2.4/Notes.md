# Problem 2.4

## Problem statement
Partition: Write code to partition a linked list around a value x, such that all nodes less than x come before all nodes
greater than or equal to x. (IMPORTANT: the partition element x can appear anywhere in the "right partition" it does not 
need to appear between the left and the right partition) The additional spacing in the example below indicates the partition.
Yes the output below is one of many valid outputs)

## Solution Attempt

### Listen
Is the linked list singly linked or doubly linked? singly!
Is the value x provided as a node or a value? value
What should i return if x isnt in the list

## Examples

{ 3 5 8 5 10 2 1 } 5 -> a solution { 3 1 2 10 5 5 8 }
{ 5 1} 5 -> {1 5}

## Brute Force
We could initialize a linked list and set any value less than the partition as the head, then any value greater as the tail
This would be done in O(n) time and O(n) space. 

## Optimize
We could do this in place by inserting less than as the head, and greater than as the tail. However this would cause infinite loop as we would always re-add. 

What if we found the value in its place, then re-looped moving greater values before x to the end, then smaller values after x to the beginning.


## Walk Through
Loop through the entire list, find the node for x and find the tail
Loop again. 
    if we haven't reached x yet and its greater than x, make prev.next = this.next. then set tail.next = to this and this.next = null
    if we have reached x and its less than x. set prev.next = this.next, set this.next = head. set head = this.

## Implement

'''
bool PartitionMyFirstAttempt(ref LinkedListNode<int> head, int x)
{
    LinkedListNode<int> it = head;
    LinkedListNode<int> tail = null;
    int xIdx = -1;
    int count = 0;
    while(it != null)
    {
        if(xIdx < 0 && it.Value == x)
        {
            xIdx = count;
        }
        count++;
        tail = it;
    }
    if(xIdx < 0 || head == null) return false;
    if(count < 2) return true;

    count = 0;
    it = head;
    LinkedListNode prev = null;
    while(it != null)
    {
        LinkedListNode<int> copy = it;
        it = it.Next;
        if(count < xIdx && copy.Value > x)
        {
            tail.Next = copy;
            if(prev != null)
            {
                prev.Next = copy.Next;
                copy.Next = null;
            }
            else 
            {
                copy.Next = head;
                head = copy;
            }
        }
        else if(count > xIdx && copy.Value < x) 
        {
            copy.Next = head;
            head = copy;
            if(prev != null)
            {
                prev.Next = copy.Next;
                copy.Next = null;
            }
        }
        count++;
        prev = it;
        it = it.Next;
    }
}

bool PartitionBest(ref LinkedListNode<int> node, int x)
{
    LinkedListNode<int> head = node;
    LinkedListNode<int> tail = node;

    while(node != null)
    {
        LinkedListNode nextCopy = node.next;
        if(node > x)
        {
            tail.next = node;
            tail = node;
        }
        else 
        {
            node.next = head;
            head = node;
        }
        node = nextCopy;
    }
    tail.next = null;
}

'''

## Test


## Notes. 
- Got too careful about copying. Its not that complicated!
- I didn't need to use the actual tail. I could have made the first node the head. Would have been much simpler.