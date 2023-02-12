# Problem 1.6

## Problem statement
Implement a method to perform basic string compression using the counts of repeated characters. For example, 
the string aabcccccaaa would become a1b1c5a3. If the compressed string would not become smaller than the original string,
you should return the original string. You can assume there are only uppercase and lowercase letters.

## Solution Attempt

### Listen
Only letters. 
ASCII characters. 

## Examples

"aabcccccaaa" -> a2b1c5a3
"abc" -> "abc"

## Brute Force
A brute force solution would be to use a stringbuilder, loop through the string counting the repeating characters, 
comparing to the previous character, then when the character changes pop that onto the string with the count. At the end 
you could compare the input string with the stringbuilder length, then return which ever is smaller.
This would use O(n) time and O(n) space. 

## Optimize
We are going to have to loop through the string regardless. So improving on O(n) isn't possible. 
If we didnt have to return the original string (if its not smaller) Then we could use the input string allocation O(1)
However it would be strange to build the compressed string then undo it if we determined its not longer. 
We could allocate an array of ints indexed by characters with their counts. 
While building that array we can generate a length of the compressed string. Then loop through again to make the string smaller.
Why not just allocate a new string of size n though? 
The question for the interviewer is it can be solved each way, Depending on the system, the fresh allocated string might be cleaner
code. If the memory allocation could be O(n) at larger sizes, then we should consider using the array counts.
Lets use the allocated string

## Walk Through
Allocate a compressed string matching the length of the input string. It doesnt need to be larger for the null terminator
create a local variable character to hold what character we are counting
create an index variable for the output string set to 0.
for each character in the input string
    if this isnt the first character, put the last count in the output string index and iterate it.
    if its not equal to the currently tracked character, insert that char to the output str and iterate the index
    if the output string index is at the end, return the input string. 
insert a null terminator and return the output string

## Implement

'''
char[] StringCompression(char[] toCompress)
{
    char lastChar = '\0';
    char[] compressed = new char[toCompress.Length];
    int outIdx;
    int compressedCount; 
    for(int i = 0; i < toCompress.Length; i++)
    {
        if(outIdx >= toCompress.Length) return toCompress;
        else if(toCompress[i] != lastChar)
        {
            if(i > 0)
            {
                //encode the count
                int numDigits = (int)Math.log10(compressedCount) +1;
                int idxOffset = numDigits;
                for(int i = 1; i <= numDigits; i++)
                {
                    compressed[outIdx + idxOffset] = (char)((int)'0' + (compressedCount % (int)Math.Pow(10, i)));
                    idxOffset--;
                }
                outIdx += numDigits;
                compressedCount = 1;
            }
            compressed[outIdx++] = toCompress[i];
            lastChar = toCompress[i];
        }
        else 
        {
            compressedCount++;
        }
    }
    compressed[outIdx++] = '\0';
    return compressed;
}
'''

## Test
"aabcccccaaa"
a not equal to \0, i is 0 -> "a"
a is equal to a, compressedCount is 2.
b not equal to a, num digits is 1. 2%10 is 2. 2 is encoded into index 1 of compressed
... 



## Notes
- Perhaps ask the cost of array allocation. 
- I think i solved this better than the solution (no stringbuilder)
- It would have been easier if i preallocated a stringbuilder though.
- Int to string is apparently O(1) runtime. 