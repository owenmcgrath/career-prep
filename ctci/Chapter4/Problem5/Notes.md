# Problem x.x

## Problem statement

Implement a function to check if a binary tree is a binary search tree

## Solution Attempt

### Listen

can the binary tree be null? yes
Yes to duplicates? yes they can be to the right.

## Examples
    4   
1       3       False!

    4
1       6       True

## Brute Force
We could traverse through the tree checking if the left child is less than and the right child is greater than. 
on each comparing the outcome with the previous outcome and returning.

## Optimize

This is O(n) traversal and O(1) space. I dont think it can be more optimal.

It might make sense to preorder traverse, that way we don't need to do extra traversing if necessary

## Walk Through


bool valid = true
valid = valid && (left is null or left is less than this)
valid = valid && (right is null or right is greater than this)
if(!recurseLeft) return false;
if(!recurseRight) return false;

## Implement

'''
bool ValidateBST(TreeNode root)
{
    if(root == null) return true;
    bool valid = true;
    if(root.left != null) valid = root.left < root.val;
    if(root.right != null) valid = valid && root.right >= root.val;
    if(!valid) return false;
    if(!ValidateBST(root.left)) return false;
    if(!ValidateBST(root.right)) return false;
}
'''

## Test


## Notes. 
- I did this wrong, didnt handle the case where the node is in the wrong spot. 