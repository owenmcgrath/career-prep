# Problem 1.3

## Problem statement
Write a method to replace all spaces in a string with '%20'. You may assume the string has additional space at the end
and that you are given the true length of the string. The true length of the string removes trailing spaces etc.

## Solution Attempt

### Listen
Assuming ASCII characters
Assuming non-nullable strings
Underscores don't count as spaces

## Examples

"Mr John Smith    ",13
" ab c  ", 6

## Brute Force
loop through the string. Remove the character at the space then insert "%20". Return the string

## Optimize
Many array copies are space hungry.. we want to avoid copies/inserts/removes

What if we looped through the string up to the "true" length, counting the spaces, then allocated a string with length
true length + 2*numspaces (replacing % with the space then adding two more characters)
then loop through, add the %20 for the space

This appears to be space optimal and time optimal O(n) O(1)

REDO contains sufficient space
We don't need to allocate a new array, there is sufficient space in the input string
Keep to indexes, the initial one being the "true" length -1, the other being the input string length - 1
Iterate backwards, copying the characters if its not a space. Decrementing 3 times and copying %20 if it is!

## Walk Through

loop through string up to true length and count the spaces.
allocate an array with true length + 2* numspaces
loop through the string, with a floating index for the allocated array
return the allocated array

Keep to indexes, the initial one being the "true" length -1, the other being the input string length - 1
Iterate backwards, copying the characters if its not a space. Decrementing 3 times and copying %20 if it is!

## Implement

'''
char[] URLify(char[] str, int trueLen)
{
    int numSpaces = 0;
    for(int i = 0; i < trueLen; i++)
    {
        if(str[i] == ' ') numSpaces++;
    }
    char[] url = new char[trueLen + (2*numSpaces)];
    int outIdx = 0;
    for(int inIdx = 0; inIdx < trueLen; inIdx++)
    {
        if(str[inIdx] == ' ')
        {
            url[outIdx++] = '%';
            url[outIdx++] = "2";
            url[outIdx++] = "0";
        }
        else 
        {
            url[outIdx++] = str[inIdx];
        }
    }
}

char[] URLifyRedo(char[] str, int trueLen)
{
    int strIdx = str.Length - 1;
    for(int trueIdx = str.Length; trueIdx > -1; trueIdx--)
    {
        if(str[trueIdx] == ' ')
        {
            url[outIdx--] = "0";
            url[outIdx--] = "2";
            url[outIdx--] = "%"
        }
        else 
        {
            url[outIdx--] = str[inIdx];
        }
    }
    return str;
}

'''

## Test

"Mr John Smith    ",13
2 spaces. Allocating array of 17 characters
M M
Mr Mr
Mr  Mr%20
Mr J Mr%20J
Mr Jo Mr%20Jo
Mr Joh Mr%20Joh
Mr John Mr%20John
Mr John Smith Mr%20John%20Smith. 17 characters. Good!

" ab c " 
3 spaces. Allocating array of 12
" " "%20"
" a" "%20a"
" ab" "%20ab"
" ab " "%20ab%20"
" ab c" "%20ab%20c"
" ab c " "%20ab%20c%20" 12 characters. Good!

## Notes. 
- Had to check the indexing thing at the end. 99% sure
- Misunderstood additional space. Rewriting to handle that
- Questions I should have asked:
    1. Does "sufficient space" mean the input string is the exact size of the output"
    2. If not, should i use a null terminator for string ending?
- Split up the functions, two different things happen here!