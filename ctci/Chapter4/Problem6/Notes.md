# Problem 4.6

## Problem statement

Write an algorithm to find the "next" node (i.e. in-order successor) of a given node in a binary search tree. You may assume
each node has a link to its parent. 

## Solution Attempt

### Listen

Can i receive null nodes? yes
Can i assume integers? yes.


## Examples

            5
    3               7
2       4       6       8

## Brute Force

This problem seems to be checking a bunch of conditionals and maybe looping through the parents.
if the right child isnt null, its the right child
else loop through the parents until the parent is greater than the value.
if we get to the top of the node then the parent is null.

## Optimize

This is done in Logarithmic time and constant space. It likely doesn't get better than that.

## Walk Through

## Implement

'''
TreeNode Successor(TreeNode source)
{
    TreeNode retVal = source;
    if(source.right != null)
    {
        while(retVal.left != null)
        {
            if(retVal.left == null) return retVal;
        }


    }
    int val = source.val;
    while(retVal != null)
    {
        if(retVal.parent.val > val) return retVal.parent;
        retVal = retVal.parent;
    }
    return retVal;
}

'''

## Test


## Notes. 
- missed the case that it should be the one all the way to the left of the right child subtree