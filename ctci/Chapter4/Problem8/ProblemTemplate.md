# Problem 4.8

## Problem statement
First Common Ancestor: Design an algorithm and write code to find the first common ancestor of two nodes in a binary tree. 
Avoid storing additional nodes in a data structure. NOT this is not necessarily a BST.

## Solution Attempt

### Listen

Null trees? yes
Return null if no shared nodes? yes.
can I use integers as the value of the binary tree? yes
Can the nodes have links to parents? no
Can we assume the provided nodes are part of the tree? no
Are we provided the root? yes.

## Examples

                3
        5               1
    2       6       0       8
7       4

5 and 1 -> 3
5 and 4 -> 5

## Brute Force

We could traverse each child and report which side a and b are on. If there is one on each side than this is the common root.
If one isnt in the tree return null.

This is done in n^2 time.  

## Optimize

We should be able to knock this down to O(n) time with some traversal magic.
If we start with a preorder traversal we can check if we are one of the nodes. 
If we are, sweet, do a preorder traversal on that node to see if the other is a child. 
if it is return a.
if its not, continue the existing search until we find the other node, by searching the right tree of everything we saw above. 

## Walk Through


## Implement

'''

TreeNode FirstCommonAncestor(TreeNode root, TreeNode a, TreeNode b)
{
    if(root == null) return null;
    if(root == a || root == b) return root;
    TreeNode left = FirstCommonAncestor(root.left, a, b);
    TreeNode right = FirstCommonAncestor(root.right, a, b)l
    if(left != null && right != null) return root;
    if(left == null && right == null) return null;
    return left != null ? left : right;
}

'''

## Test


## Notes. 
- Really tricky and did poorly