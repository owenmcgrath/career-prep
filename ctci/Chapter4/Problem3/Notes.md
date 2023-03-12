# Problem 4.3

## Problem statement

List of Depths: Given a binary tree, design an algorithm that creates a linked list of all the nodes at each depth. 

## Solution Attempt

### Listen

Should the return value be a list of LinkedLists? We can't really assume anything about the balance of the tree, so might have to. 
Do the linked lists need to be in any order? no. 
Can I use System.Collections.List ? yes
Can I use System.Collections.LinkedListNode<> ? yes

## Examples
    3
9       20              becomes [[3], [9 -> 20], [15-> 7]] OR [[3], [20 -> 9], [7 -> 15]]
    15      7  

## Brute Force

You could do a post order traversal tracking the depth as a parameter, instantiating a new linked list for each new depth.

## Optimize

A preorder traversal would probably do better here as you wont have to handle the indexed gaps in the list. 
i.e. when i reach a depth i can check if its greater than the length of the List of linked lists and then append to it. 

This problem seemed to easy using C# Linked Lists, should solve this using LinkedListNode and tracking the appends.

This likely means we need to treat this as a breadth first search for each depth index.

With O(n) space we could do a traversal and throw everything in a hashmap then push everything into a linkedlist at the end.

this would use 2n space but n time. as DFS 

We could also use a queue, that would use O(2n) space and O(n) time.

DFS is probably better here as we need to cover all the bases anyway and the code will probably be cleaner in the end. 
(will be a nice clean recursive algorithm)

## Walk Through
initialize a hashmap of treenodes
recurse through the tree, with a depth index
    throw the treenode at the depth index on the hashmap


## Implement

'''

List<LinkedListNode<T>> ListOfDepths<T>(TreeNode root)
{
    List<LinkedListNode<T>> list = new List<LinkedListNode<T>>();

}

void ListOfDepths<T>(TreeNode root, int depth, ref List<LinkedListNode<T>> list)
{
    if(root == null) return;
    if(depth > list.Length) list.Add(new LinkedListNode<T>());
    list[depth].AddToEnd()
}

'''

## Test


## Notes. 

I overthought this and was right with my first approach, using System.Collections.LinkedList would have been fine, 
their solution was also the same. 