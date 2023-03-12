# Problem 4.11

## Problem statement
You are implementing a binary search tree class from scratch which in addition to insert, find and delete has a method
getRandomNode() which returns a random node from the tree. All nodes should be equally likely to be chosen. Design and implement 
an algorithm for getRandomNode and explain how you would implement the rest of the methods. 

## Solution Attempt

### Listen

## Examples

## Brute Force

## Optimize

## Walk Through

For insert, you start at the root.
If root is null, instantiate a new node and make it this value. 

If the inserted value is greater than (or equal to) the current node, 
    if the right is null, instantiate and make this value the node value
else recurse to the right. 

if the inserted value is less than the current node
    if the left is null instantiate and make this value the node value.
else recurse to the left.

For find, we can implement a depth first approach or a breadth first approach. These have similar run times but I would 
consider other factors to chose. For the sake of simplicity we will implement a breadth first preorder traversal.

starting with the root
check if the current node equals the value being searched for. If so return it.
if recursing to the left isnt null, return it.
if recursing to the right isnt null, return it.

for delete:
First find the parent by traversing through the tree (as described above) and checking if either left or right holds the child. 
if both child nodes are null, set whichever child this is to null.
if there is only one child, replace the deleted node with that child
else find the inorder successor and replace the in order successor with that, deleting where the inorder successor previously was.

For get random nodes there are two ways to do this.

Since we are implementing the class its safe to assume we are tracking the number of nodes that we have implemented. We could use a random number generator from 0 to n and traverse that number of times to get the value. 

This would occur in O(n) runtime. 

Could we do this in O(logn) runtime? I think we could but would sacrifice the means of "equally likely to be chosen"
We could use a random number generator to generate a depth, and then a random boolean every step to know which direction to move. 
Problem is if the binary search tree is unbalanced we could get stuck. 

## Implement

'''
public class MyBstNode<T>
{
    public T val;
    public MyBstNode<T> left;
    public MyBstNode<T> right;

    public MyBstNode<T>()
    {

    }
}

public class MyBst<T>
{
    private List<MyBstNode<T>> NodeList;

    public MyBstNode<T> Root {get; private set;}

    public void insert(T value)
    {

    }

    public MyBstNode<T> find(T value)
    {

    }

    public void delete(MyBstNode<T> node)
    {

    }

    public MyBstNode<T> getRandomNode()
    {
        System.Random r = new System.Random();
        r.GetNextInt(0, NodeList.Count);
        int count = 0;
        return TraverseNTimes(root, ref count, ref NodeList.Count);
        

    }

    private MyBstNode<T> TraverseNTimes(MyBstNode<T> node, ref int count, ref int total)
    {
        if(node == null) return null;
        if(count + 1 == total) return node;
        count++;
        MyBstNode<T> result = TraverseNTimes(node.left, count, total);
        if(left != null) return left;
        result = TraverseNTimes(node.left, count + 1, total);
        if(result 1= null return result);
        return null;
        

        
    }

}

'''

## Test


## Notes. 