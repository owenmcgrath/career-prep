# Problem 1.1 

## Problem statement
Is Unique: Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?

## Solution Attempt

### Listen
All unique characters. 
Assuming this is all characters 0-255 code? 
Handle empty strings? yes

## Examples
"abc123"
"abcc123"
"c321cba"

## Brute Force

Loop through each character. Then loop backwards to check if each previous value matches that character. O(n^2) alg with O(1) space

## Optimize
We could use space to ensure that we haven't already gotten this value! So we can use a hashmap insert, and check 
contains key. This would be an O(n) algorithm with O(n) space.

What if we cant use these data structures though? 

My mind is jumping to bit math. maybe we can use the keycode to set a bit instead of using a hashmap? 
Problem is we would need a 255 bit integer which is much too large. 

What if we sort the string? Then we can check only if the previous character matches? This would be O(n*log(n)), better 
than the brute force O(n^2)

## Walk Through

Initialize a hashmap, loop through each character and check if it is in the hashmap. if theres a contain return false. 
At the end of the loop, return true!

For brute force, loop through each character, then loop backwards checking if theres a match

## Implement

'''
bool IsUniqueHash(string str)
{
    if(str == null) return true;
    HashSet<char> hashMap = new HashSet<char>();
    for(int i = 0; i < str.Length; i++)
    {
        if(hashMap.Contains(str[i])) return false;
        hashMap.Insert(str[i]);
    }
    return true;
}

bool IsUniqueSort(string str)
{
    if(str == null) return true;
    Array.Sort(str);
    for(int i = 1; i < str.Length; i++)
    {
        if(str[i] == str[i-1])
        {
            return false;
        }
    }
    return true;
}
'''

## Test

Adding a non sorted string to test the sort version

Caught the null check! added that in

All tests work as expected!

## Notes. 
1. Had to google if strings are nullable in C#
2. Caught sorting late
3. Forgot semicolon on hashmap insert
4. Wrong sort syntax. Array.Sort(str) instead of str.Sort()

FROM THE SOLUTION
1. Ask the interviewer ASCII or unicode? this will give you a value for the length check. (128 or 256)
2. Array would be better than a hashset here, no Dynamically allocated memory issues
3. If the number is greater than max ascii/unicode characters return
4. Could use bit math if only lowercase characters. 
5. I got the "no extra data" correct