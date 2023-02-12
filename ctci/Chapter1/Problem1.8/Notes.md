# Problem 1.8

## Problem statement

Write an algorithm such that if an element in an MXN matrix is 0, its entire row and column are set to 0

## Solution Attempt

### Listen
Assume non-nullable array
Assume no empty array

## Examples

[[0,1,1],[1,1,1],[1,1,0]] -> [[0,0,0],[0,1,0],[0,0,0]]

## Brute Force

We could initialize two hashsets of rows and columns that need to be zero'ed out.
Loop through each element and append to the hashset
Then write those values to each hashset

This is O(M*n) time and O(m+n) space

## Optimize

Time cannot be improved here but can we make this in place and with no hashset?
We need to know if we have zero'ed out the row or column previously to skip it. Since its rectangular it gets complicated
We could use a single hashset of just columns which is a marginal optimization

I got a hint about using the matrix itself for data storage
Perhaps I could overwrite values to be overwritten of the row and column?

What if...
we used the first zero index that appears, we fill row numbers in the column to be zero'ed, then column numbers in the row to be zero'ed
We'll have to search that row again. How about we mark one dimension with just a 1, then the other with a value


## Walk Through
initialized variables. 
columnStoreX -> x value of first found zero
rowStoreY -> y value of the first found zero
foundZero -> true if we found the first zero value
loop through each x
    loop through each y
        is it zero?
            if we found zero, 
                in the store row set that row (in the column) to 1, set that column in the row to 1
            if not, set the whole column and row to zero and set foundZero to true set x,y to 1
loop through each columnStoreX
    for 0 to n set that row to zeros, skipping the store row
loop through each columnStoreY
    for 0 to M set each column to zeros, skipping the store column



## Implement

'''
public int[,] ZeroMatrix(int[,] matrix, int m, int n)
{
    int columnStoreX = 0;
    int rowStoreY = 0;
    bool foundZero = false;
    for(int x = 0; x < m; x++)
    {
        for(int y = 0; y < n; y++)
        {
            if(matrix[x,y] == 0)
            {
                if(foundZero)
                {
                    matrix[columnStoreX,y] = 0;
                    matrix[x,columnStoreY] = 0;
                }
                else 
                {
                    foundZero = true;
                    columnStoreX = x;
                    rowStoreY = y;
                }
            }
        }
    }

    for(int x = 0; x < m; x++)
    {
        if(matrix[x, rowStoreY] == 0)
        {
            for(int y = 0; y < n; y++)
            {
                if(y != rowStoreY) matrix[x2, y] = 0;
            }
        }
    }

    for(int y = 0; y < n; y++)
    {
        if(matrix[columnStoreX, y] == 0)
        {
            for(int x = 0; x < m; x++)
            {
                matrix[x, y] = 0;
            }
        }
    }
}

'''

## Test


## Notes. 
- Could have been more efficient just by marking rows with a zero instead of a 1
- Needed a hint here for space efficiency. Remember to recycle array space in these types of problems