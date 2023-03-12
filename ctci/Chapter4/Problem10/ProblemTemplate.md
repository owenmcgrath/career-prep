# Problem 4.10 

## Problem statement

T1 and T2 are two very large binary trees where T1 is much bigger than T2. Create an algorithm to determine if T2 is a
subtree of T1. A tree T2 is a subtree of T1 if there exists a node n in T1 such that the subtree of n is identical to
T2. That is if you cut off the tree at node n the two trees would be identical.

## Solution Attempt

### Listen

Does very large mean that we can assume they cant be null? yes
Does identical mean its the same node in the tree? or are they the same values? just same values, its not part of the tree.
 
## Examples
        T1                  T2      TRUE!
        3                   4
    4       5             1   2
1       2

        T1                  T2      FALSE!
        3                   4
    4       5             1   2
1       2

## Brute Force

First find the root of T2 in T1. 
Then inorder traverse through each child of the tree, returning false if the values arent equal, and true if they are equal.

## Optimize

The initial problem says its a "large binary tree". Since binary trees have no order and theres no information about the balance 
of the binary tree, we can't try to do any tricks to more quickly find the root. 

This would be done in O(m + n) time and constant space.

## Walk Through

simultaneous traverse
    if theyre both null return true.
    if T1 is null return false
    if T2 is null return false
    if(!recurse both left) return false
    if(!recurse both right) return false
    return T1.val == T2.val


recurse left of t1
check if this node is the t2 root. if so,
    run the simultaneous traverse through both trees, return the result.
recurse right

## Implement

'''

TreeNode FindT2(TreeNode T1, TreeNode T2)
{
    TreeNode retVal = FindT2(T1.left, T2);
    if(retVal != null) return retVal;
    if(T1.val == T2.val) return T1;
    retVal = FindT2(T1.right, T2);
    if(retVal != null) return retVal;
    return null;
}

bool CompareTree(TreeNode a, TreeNode b)
{
    if(a == null && b == null) return true;
    else if(a == null || b == null) return false;

    if(!CompareTree(a.left, b.left)) return false;
    if(a.val == b.val) return true;
    else return false;
    if(!CompareTree(a.right, b.right)) return false;
    return true;
}


bool CheckSubtree(TreeNode T1, TreeNode T2)
{
    TreeNode T1Subtree = FindT2(T1);
    if(T1Subtree == null) return false;
    return CompareTree(T1Subtree, T2);
}

'''

## Test


## Notes. 

I solved it right. 

With big, need to remember the callstack space usage with recursion and the 