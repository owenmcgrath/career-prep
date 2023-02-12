# Problem 1.7

## Problem statement
Given an image represented by an NxN matrix, where each pixel in the image is represented by an integer, write a method
to rotate the image by 90 degrees. Can you do this in place?

## Solution Attempt

### Listen
What does in place mean? - dont use any space
Clockwise or CCW? Assuming clockwise

## Examples

{{1,2},{3,4}} -> {{3,1},{4,2}}
{{1,2,3}, {4,5,6}, {7,8,9}} -> {{7,4,1},{8,5,2},{9,6,3}}

listing out coordinate swaps to look for pattern
{0,0} -> {2,0}
{2,0} -> {2,2}
{2,2} -> {2,0}
{2,0} -> {0,0}

{1,0} -> {1,2}
{1,2} -> {2,1}
{2,1} -> {0,1}
{0,1} -> {1,0}

and so on and so on.

## Brute Force

Initialize an empty array of the same size. 
Traverse function to generate output coordinates for a 90 degree rotation
    determine what "ring" you are on by finding the closest edge. Its the minimum of x-0, n-x, y-0, n-y
    iterating n-1 times
    at ring zero you are traversing on the edge 0 to n
    at ring one you are traversing the edge 1 to n-1... etc etc

    onRightEdge = x == n - ringNum
    onLeftEdge = x == ringNum
    onBottomEdge = y == n - ringNum
    onTopEdge = y == ringNum
    
    if on the right edge
        if on the bottom edge decrement x
        increment y
    if on the left edge
        if on the top edge increment x
        decrement y
    if on the top edge
        increment x
    if on the bottom edge
        decrement x

for i = 0 to n
    for j = 0 to n
        x,y = traverse(i,j)
        out[x,y] = in[i,j]
    

## Optimize

Bruteforce time here is O(n) where n is the total matrix elements
Bruteforce space is O(n) also. This can be done in place by changing it so that we store a local variable to hold the 
last rotation

There are some marginal optimizations i could make, like making the edge parameters into the traverse function, that way 
you dont have to regenerate the ring number every time. However this would make iteration awkward to read. Im suggesting 
We regenerate the ring number every time for readability

Now that im thinking of it its easier to iterate by ring number and then iterate from 1 to n - 1, 2 to n - 2 etc 
so i will parameterize the edges and the ring number

## Walk Through

For NxN matrix there are n/2 (rounded up) rings. 
initialize a local variable for the stored traversal
iterate from 0 to that total ring count
    loop from 0 + ring count to n - ring count
        run the traverse and store the traversed value. 
        set the current iteration to that traversed value



## Implement

'''
public void Traverse(int[,] matrix, int n, int ringNum, int leftEdge, int rightEdge, int x, int y, out int newX, out int newY)
{
    newX = x;
    newY = y;
    for(int i = leftEdge; i < rightEdge; i++)
    {
        bool onRightEdge = x == n - 1 - ringNum;
        bool onLeftEdge = x == ringNum;
        bool onTopEdge = y == ringNum;
        bool onBottomEdge = y == n - 1 - ringNum;
        if(onRightEdge)
        {
            if(onBottomEdge) newX--;
            else newY++;
        }
        else if(onLeftEdge)
        {
            if(onTopEdge) newX++;
            else newY--;
        }
        else if(onTopEdge) newX++;
        else if(onBottomEdge) newX--;
        
    }
}

public void RotateMatrix(int[,] matrix, int n)
{
    bool oddN = n % 2 == 1;
    int ringCount = oddN ? (n / 2) + 1 : n/2;
    int storedValue = 0;
    int storedValueCopy = 0;
    for(int i = 0; i < ringCount; i++)
    {
        if(i == ringCount - 1 && oddN) continue; //center
        for(int topX = i; topX < (n-i); topX++)
        {
            int travX, travY;
            Traverse(matrix,n,i,i,n-i,topX, i, out travX, out travY);
            storedValue = matrix[travX,travY];
            matrix[travX,travY] = matrix[topX,i];

            storedValueCopy = storedValue;
            Traverse(matrix,n,i,n-i, travX, travY, out travX, out travY);
            storedValue = matrix[travX,travY];
            matrix[travX,travY] = storedValueCopy;

            storedValueCopy = storedValue;
            Traverse(matrix,n,i,n-i, travX, travY, out travX, out travY);
            storedValue = matrix[travX,travY];
            matrix[travX,travY] = storedValueCopy;

            storedValueCopy = storedValue;
            Traverse(matrix,n,i,n-i, travX, travY, out travX, out travY);
            storedValue = matrix[travX,travY];
            matrix[travX,travY] = storedValueCopy;
        }
    }

}

'''

## Test

testing the 2x2 looks good!
testing the 3x3



## Notes. 
- The traverse code is extra but its the right idea. Could have just copied even though it didnt change the time efficiency
- Code would have been more optimal