# Problem 1.2

## Problem statement
Given two strings write a method to decide if one is a permutation of another

## Solution Attempt

### Listen
ASCII or unicode? ASCII
can the strings be null? no
If by permutation do you mean that the characters can be re-arranged to be the same string?

## Examples

"abc" "dcg"
"abc" "cab"

## Brute Force
loop through each character in string a, loop through each character in string b and see if that character is there, if so 
remove from the second string. 
if its not there, its not a permutation. If its there return true! O(m^2*n^2) time

## Optimize
Removing a character does an array copy every time which is pricy. 
What if we put each in a hashmap O(m+n), then looped again to see if there was a match?
This would be O(m+n) time which is essentially O(n) because m and n have to be equal. This would be O(n) space as well

If we wanted to do O(1) space.
We could sort the arrays O(nlog(n)) then do a loop check

Could we retain O(n) time with O(1) space?
We can't do anything with bitmath because there is no uniqueness of characters
We could allocate two arrays of integers of size 255. Then tally each character in each string.
If the tallies all match then this works!
A hashmap would work here as well but this would be O(n) space

## Walk Through

break out if the sizes dont match
initialize two arrays of integers of size 255
loop through m, increment the m array by 1 at the index of the character value
Repeat for n.

loop 0 through 255-1, check if the tallies from m and n are equal. 
if theres a mismatch return false, else return true!

## Implement

'''
bool CheckPermutation(string a, string b)
{
    if(a.Length != b.Length) return false;

    int[] aTally = new int[byte.MaxValue];
    int[] bTally = new int[byte.MaxValue];
    for(int aIdx = 0; aIdx < a.Length; aIdx++)
    {
        aTally[(int)a[aIdx]]++;
    }
    for(int bIdx = 0; bIdx < b.Length; bIdx++)
    {
        bTally[(int)b[bIdx]]++;
    }

    for(int i = 0; i < byte.MaxValue; i++)
    {
        if(aTally[i] != bTally[i]) return false;
    }

    return true;
}
'''

## Test

"abc" "dcg"

aTally looks like { a:1, b:1, c:1 }
bTally looks like { d:1, c:1, g:1 }

on the "a" iteration aTally != bTally return false! Correct!

"abc" "cab"

aTally looks like { a:1, b:1, c:1 }
bTally looks like { a:1, b:1, c:1 }

all match return true! Correct!

"abbc" "bacb"
aTally looks like { a:1, b:2, c:1 }
bTally looks like { a:1, b:2, c:1 }

all match return true! Correct!


## Notes
1. Had to google what a permutation is
2. Get parameter name straight. Either m,n or a,b
3. Ask about whitespace and case sensitivity. Didnt ask that
4. Didnt need to instantiate two arrays, could have decremented on the second loop. Thought its constant
5. Even though the efficiency didnt change, it is still better. Think beyond Big O