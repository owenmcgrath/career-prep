# Problem 4.4

## Problem statement

Check balanced: Implement a function to check if a binary tree is balanced. For the purposes of this question a balanced tree
is defined to be a tree such that the heights of the two subtrees of any node differ by more than one. 

## Solution Attempt

### Listen

Can the root be null? yes

## Examples
    2
1       3       TRUE!

1
    2
        3       FALSE!

## Brute Force

The best way to do this is calculate the length of the subtrees recursively then compare them for each node in the list. 
For this we want to do a DFS tracking upwards the length of the tree. 

## Optimize

This is a O(n) traversal through each of the nodes. This is as fast as it will go. Since we need to traverse each subtree 
anyway, a BFS search doesn't make sense here. 

## Walk Through

param size, parent
if the left child and right child are null, size + 1. 
int leftSize = recurse left with size 0 and left child
if(leftSize == -1) return -1;
int rightSize = recurse right with size 0 and right child
if(rightSize == -1 || abs(leftSize - rightSize) > 1 ) return -1;
else return 1 + leftSize + rightSize;

## Implement

'''
bool CheckBalanced(TreeNode root)
{
    return BalancedTreeSize(root, 0) != -1;
}

//return -1 if not balanced
int BalancedTreeSize(TreeNode root, int size)
{
    if(root == null) return 0;
    int leftSize = CheckBalanced(root.left, 0);
    if(leftSize == -1) return -1;
    int rightSize = CheckBalanced(root.right, 0);
    if(rightSize == -1 || abs(leftSize - rightSize) > 1) return -1;
    else return 1 + leftSize + rightSize;
}


'''

## Test


## Notes. 