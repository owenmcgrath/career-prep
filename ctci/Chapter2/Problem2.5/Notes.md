# Problem 2.5 

## Problem statement

Sum List: You have two numbers represented by a linked list where each node contains a single digit. The digits are stored
in reverse order such that the 1s digit is at the head of the list. Write a function that adds the two numbers and returns 
the sum as a linked list (you are not allowed to cheat and convert the linked list to an integer)

Suppose they are also in a forward order. Solve that as well.

## Solution Attempt

### Listen

Assuming single digit.
Can linked lists be empty? no!
singly linked? yes
Leading zeros? yes

## Examples

Part A: (7->1->6) + (5->9->2) output is 2->1->9
Part B: (6->1->7) + (2->9->5) output is 9->1->2

## Brute Force

For part A, you can create a linked list. Looping through each iteration and carrying a value over to add to the sum of the two indices.
If you have reached the end of one and not the other you can just add 0. This is done in O(m + n) time and O(m + n) space.

## Optimize
This can be done mostly in place to get rid of the space requirement. But you'd have to find the one with the largest length and work off of that. It's guaranteed that you won't have to instantiate. 

Should we do that? Yeah its more optimal

## Walk Through
Part A:
Calculate the lengths of each linked list while getting the tails.
if a is longer than b, set the tail of a equal to the head of b, and vice versa. Also get a reference to the head of the combined list,
and the head of the added list

count loop up to the length of the reference length
    sum: the ref value, the toAdd value (if not null) and the remainder from the previous iteration.
    the remainder for the next iteration is the sum divided by 10;
    the digit to insert at the ref node is sum % 10
    increment the toAdd, increment the reference.

set the ref next to null

Part B: Since we can't sequentially carry over the remainder, as we'd have to track 1 to n pointers in a singly linked loop
This will need to be solved with recursion


## Implement

'''
LinkedList<byte> SumListA(LinkedListNode<byte> a, LinkedListNode<byte>b)
{
    int lenA = 1;
    int lenB = 1;
    LinkedListNode<int> aIt = a;
    LinkedListNode<int> bIt = b;
    while(aIt.Next != null)
    {
        aIt = aIt.Next;
        lenA++;
    }
    while(bIt.Next != null)
    {
        bIt = bIt.Next;
        bIt++;
    }

    bool aFirst = lenA > lenB;
    LinkedListNode refHead;
    LinkedListNode addHead;
    int refLen;
    if(aFirst)
    {
        refHead = a;
        aIt.next = b;
        refLen = lenA;
        addHead = b;
    }
    else 
    {
        refHead = b;
        bIt.next = a;
        refLen = lenB;
        addHead = a;
    }

    int remainder = 0;
    for(int i = 0; i < refLen; i++)
    {
        int addHeadValue = 0;
        if(addHead != null)
        {
            addHeadValue = addHead.Value;
            addHead = addHead.Next;
        }
        int newVal = (refHead.Value + addHeadValue + remainder) % 10
        remainder = (refHead.Value + addHeadValue + remainder) / 10;
        refHead.Value = newVal;
        refHead = refHead.Next;
    }
    refHead.Next = null;
}

LinkedList<byte> SumListB(LinkedList<byte> a, LinkedList<byte>b)
{
    LinkedListNode<int> aTail = a;
    while(aTail.next != null) aTail = aTail.next;
    aTail.next = b;
    AddNexts(a, a, b);
    return a;
}

int AddNexts(LinkedList<byte> ref, LinkedList<byte>a, LinkedList<byte> b)
{
    int sum = 0;
    bool aNull = a.Value == null;
    bool bNull = b.Value == null;
    if(!aNull)
    {
        sum+= a.Value;
        a = a.Next;
    }
    if(!bNull)
    {
        sum+= b.Value;
        b = b.Next;
    }

    if(aNull & bNull) return 0;
    int remainder = AddNexts(ref.Next, a , b);
    ref.Value = (sum + remainder) % 10;
    return AddNexts(ref.Next, a, b) / 10;
}

'''

## Test


## Notes. 
- Didnt catch leading zeros. 
- I solved this without using memory. Im certain Part B doesnt work but Part A should work. Its important to ask the interviewer if I should try to conserve space or not.
- 