# Problem 2.1

## Problem statement
Remove Dups: Write code to remove duplicates from an unsorted linked list

## Solution Attempt

### Listen
Is this singly linked our doubly linked?
What data type should be the linked list object? (int)
Do you delete the original value? yes
can head be null? yes

## Examples

1 -> 2 -> 2 -> 1 => {}
1 -> 2 -> 3 -> 2 => {1,3}

## Brute Force
O(n^2) time and O(1) space would be to nested loop and find matches of first ptr to second ptr. Remove both if theyre equal

## Optimize
Sorting the list takes O(nlogn) time. We could sort then loop through once. This would take O(nlogn) time and O(1) space
The problem suggests we use a temporary buffer that uses space. We could create a second Linked List that we treat like a binary tree.
Binary tree insertion takes O(logn) time, n times. Then we have O(nlogn) time and O(n) space. Less optimal but uses a buffer
Using a hashtable this can be done in O(n) time and O(n) space.

## Walk Through
With buffer:
Create a dictionary of key, int. increment for each value
loop through the linked list, increment the value for each int
loop through the linked list again, checking if the value is greater than 1, and removing the value if so

Without buffer:
do a nested loop through all nodes
    loop from node to end
    if theres a match and this node, remove this node
    if the i node hasnt been removed yet remove that node

## Implement

'''
public class Node
{
    int Value;
    Node Next;
}

void RemoveSinglyLinkedNode(ref Node prev, ref node current)
{
    if(prev == null && it.Next != null) //beginning of the list
    {
        //this is the first index, set head to next, keep prev null
        it = it.Next;
    }
    else if(it.Next != null)
    {
        prev.Next = it.Next;
    }
    else if(prev != null) //end of the list
    {
        prev.Next = null
        return;
    }
}

void RemoveDupHashSet(ref Node head)
{
    if(head == null) return;
    if(head.Next == null) return; //length 1
    Dictionary<int,int> nodeCountSet = new Dictionary<int,int>
    Node it = head;
    while(it != null)
    {
        set[it.Value]++;
        it = it.Next;
    }

    it = head;
    Node prev = null;
    while(it != null)
    {
        if(nodeCountSet[it.Value] > 1)
        {
            RemoveSinglyLinkedNode(prev, it);
        }
    }
}

void RemoveDupNoBuffer(ref Node head)
{
    if(head == null) return;
    if(head.Next == null) return;
    Node it = head;
    Node prev = null;
    Node next = null;
    Node nestPrev = null;
    while(it != null)
    {
        next = it.Next;
        nestPrev = it;
        while(next != null)
        {
            if(it.Value == next.Value)
            {
                RemoveSinglyLinkedNode(nestPrev, next);
                if(it != null)
                {
                    it = it.Next;
                    RemoveSinglyLinkedNode(prev, next);

                }
            }
            next = next.Next;
        }
    }
}
'''

## Test


## Notes. 
- Wouldn't have caught that you keep the original value
- didnt know sorting a linked list is O(n^2) time
- Use LinkedList<> and LinkedListNode<> but don't use prev for singly linked lists
- Get used to singly linked lists, and writing the code for inserting/removing

## Better Solution
```
void RemoveDups(LinkedListNode<int> head)
{
    HashSet<int> set = new HashSet<int>();
    LinkedListNode<int> prev = null;
    while(head != null)
    {
        if(set.Contains(head.Value))
        {
            prev.Next = head.Next;
        }
        else 
        {
            set.Add(head.Value);
            prev = head;
        }
        head = head.Next;
    }
}

void RemoveDupsNoBuffer(LinkedListNode<int> head)
{
    LinkedListNode<int> curr = head;
    while(curr != null)
    {
        LinkedListNode<int> runner = curr;
        while(runner.Next != null)
        {
            if(runner.Next.Value == curr.Value)
            {
                runner.Next = runner.Next.Next; //remove runner.next
            }
            else 
            {
                runner = runner.Next; //iterate
            }
        }
        curr = curr.Next
    }
}
```