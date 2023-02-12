# Problem 2.6

## Problem statement

Implement a function to check if a linked list is a palindrome

## Solution Attempt

### Listen

Is it a linked lists of characters? yes
Is it singly linked? yes

## Examples
{1,2,2,1} -> true
{1,2} -> false
{1,2,3,4,3,2,1} -> 1,2,3,4,

next = null
prev = 3
curr = 2

next = 3
prev = 2
curr = 1

next = 2
prev = 1
curr = null



## Brute Force
loop through throwing all in a list. two pointer increment and decrement until they are equal or one apart, and validating they are equal.
O(n) time and O(n) space. 

## Optimize

This can eb done in place O(1) space by reversing the second half of the list

## Walk Through
This requires looping through and finding the halfway point. From there, reverse the rest of the linked list, and starting 
from either the half node or the one after the half node, iterate through the rest of the list to see if they match.
Then reverse again, and return

## Implement

'''
void Reverse(LinkedListNode<int> head)
{
    LinkedListNode<int> prev = null;
    LinkedListNode<int> curr = head;
    while(curr != null)
    {
        LinkedListNode<int> next = curr.Next;
        curr.Next = prev;
        prev = curr;
        curr = next;
    }
}

bool Palindrome(LinkedListNode<int> head)
{
    int length = 0;
    LinkedListNode<int> it = head;
    while(it!= null)
    {
        length++;
        it = it.next;
    }

    int middleNodeIdx = length % 2 > 0 ? (length / 2) + 1 : length / 2;

    LinkedListNode<int> midNode = head;
    for(int i = 0; i <= middleNodeIdx; i++)
    {
        midNode = midNode.Next;
    }

    Reverse(midNode);

    LinkedListNode<int> itEnd = midNode;
    it = head;
    while(itEnd != null)
    {
        if(itEnd.Value != it.Value) 
        {
            Reverse(midNode);
            return false;
        }
        itEnd = itEnd.Next;
        it = it.Next;
    }

    Reverse(midNode);
    return true;

}
'''

## Test


## Notes. 
- This was very easy without having to be in place. 
- In Place this problem was quite difficult requiring an array reversal