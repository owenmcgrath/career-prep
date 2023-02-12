# Problem 2.2

## Problem statement
Return Kth to last: Implement an algorithm to find kth to last element of a singly linked list

## Solution Attempt

### Listen
What do i return if there is no kth to last element? null
if k is 1, does that mean the last or before the last? it means the last
Handle null? yes

## Examples

{1,2,3,4,5} k=1 return 5
{1,2,3,4,5} k=5 return 1
{1,2,3,4,5} k=6 return null
{1,2,3,4,5} k=0 return null
{} return null

## Brute Force
handle boundary conditions. If its null return null; if k <= 0 return null
Initialize a list of linkedlistnodes, loop through the linked list and add to the list, if k > n return null. else return list[k-n]
O(n) space. O(n) time.

## Optimize
We should be able to do this without using space. Since we won't know the length, we will have to loop through the entire list no matter what
We could loop once to find the length. Then loop a second time to return the node at (k-n).
We could also use a counter & two pointers to track the value k before the current iteration. This will loop less times than the previous solution.

You could make an argument that since it won't change big O time solution 2 is more readable so that should be the way to go.
I am going to implement solution 3 since it will always iterate less.

## Walk Through
handle the boundary conditions, if its null return null, if k < 1 return null
initialize two pointers, one called elemK, another called elemIt
initialize a counter. 
while elemIt isnt null
    if counter equals k set elemK to the head
    if elemK isnt null iterate elemK
    iterate counter and elemIt

return elemk



## Implement

'''
LinkedListNode KthToLast(LinkedListNode head, int k)
{
    if(head == null || k < 1) return null;
    LinkedListNode elemIt = head;
    LinkedListNode elemK = null;
    int ctr = 0;
    while(elemIt != null)
    {
        if(elemK != null) elemK = elemK.Next;
        if(ctr == k - 1) elemK = head;
        ctr++;
        elemIt = elemIt.Next;
    }
    return elemK;
}

'''

## Test

k=1
0 elemIt{1} elemK{1} 
1 elemIt{2} elemK{2}
2 elemIt{3} elemK{3} 
3 elemIt{4} elemK{4} 
4 elemIt{5} elemK{5} 

k=5
0 elemIt{1} elemK{null} 
1 elemIt{2} elemK{null}
2 elemIt{3} elemK{null} 
3 elemIt{4} elemK{null} 
4 elemIt{5} elemK{1} 


## Notes. 
I didn't note a recursive solution which would also use O(n) space. Recursion would have been "short & sweet" but not optimal