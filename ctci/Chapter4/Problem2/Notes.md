# Problem 4.2

## Problem statement

Minimal Tree. Given a sorted array (increasing order) with unique integer elements, write an algorithm to create a BST with minimal height

## Solution Attempt

### Listen
Return the binary search tree as a node? Yes
Create the BST class? no, (using how defined on leetcode)

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
```


## Examples
1 2 3 4 5 

        3
    2       4
1               5

1 2 3 4 5 6

            3
    2           5
1           4        6

1 2 3 4 5 6 7

            4
    2               6
1       3       5       7    

## Brute Force

You could create the tree from the array, then balance out the tree by looping through each child. 

i.e. Build the BST, balance so its an upside down v, then go to the left balance, then go to the right, balance. 

this is like (nlogn)^2. Can do much better than that.

## Optimize

Since we know the array is sorted already, we can build the tree by indexing properly. 
i.e. starting at the middle, inserting
insert the middle of the left half, then right half, splitting each group until you get to the end. 
This would use O(n) time and O(n) space. Since we need to insert all the values anyway it cant get faster than this. 
We also need to build a tree data structure so it cant get faster than O(n) space.

## Walk Through

We probably want two functions here, one that determines the halfway point between two indices and one that puts them on the tree recursively.


get the root as the halfway node in the tree. (n/2)
initialize the root node with that value. 
initialize left, assign to half of the left value.
initialize right, assign to the half of the right value. (recursively iterate)


## Implement

'''
void BuildMinimalTreeChild(TreeNode parent, int[] sortedArray, int startIdx, int endIdx)
{
    if(endIdx - startIdx <= 0) return;
    TreeNode child = new TreeNode();
    int middle = startIdx + ((endIdx - startIdx + 1) / 2);
    if((endIdx - startIdx + 1) % 2 == 0) middle--;
    child.val = sortedArray[middle];
    if(val < parent.val)
    {
        parent.left = child;
    }
    else 
    {
        parent.right = child;
    }
    BuildMinimalTreeChild(child, sortedArray, startIdx, middle - 1);
    BuildMinimalTreeChild(child, sortedArray, middle, middle + 1 + (middle - startIdx))
}


TreeNode MinimalTree(int[] sortedArray)
{
    if(sortedArray.Length == 0) return null;
    TreeNode root = new TreeNode();
    int middle = sortedArray.Length / 2;
    if(sortedArray.Length % 2 == 0) middle--;
    root.val = sortedArray[middle];
    BuildMinimalTreeChild(root, sortedArray, 0, middle - 1);
    BuildMinimalTreeChild(root, sortedArray, middle+1, middle.Length - 1);

}

'''

## Test

1 2 3 4 5 
5 / 2 is 2, length is odd so middle is 2. 
Root is 3.
LEFT TREE 0, 1
    middle is 1, but its even on the left, so the value to insert is 1, and inserted to the left. 
    theres not new length to insert so returning



## Notes. 

Overcomplicated this quite a bit by lack of understanding of writing recursion. Had the idea right though!

```
TreeNode CreateMinimalBst(int[]array)
{
    return CreateMinimalBst(array, 0, array.Length - 1);
}

TreeNode CreateMinimalBst(int[] array, int start, int end)
{
    if(end < start) return null;
    int mid = (start + end / 2);
    TreeNode n = new TreeNode();
    n.val = array[mid];
    n.left = CreateMinimalBst(array, start, mid - 1);
    n.right= CreateMinimalBst(array, mid+1, start);
    return n;
}
```