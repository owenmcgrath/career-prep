# Problem 1.5

## Problem statement
One Away: There are three types of edits that can be performed on strings: insert a character, remove a character, or replace a character
Given two strings write a function if they are zero or one edits away!

## Solution Attempt

### Listen
Only moves are insert,remove,replace
assume no null strings
Assume case insensitive, 

## Examples
pale, ple -> true
pales, pale -> true
pale, bale -> true
pale, bake -> false

## Brute Force
Since we check for string length, the alg runs with abs(m-n) <=1, therfore approximate m,n to just n for length

if the check string len is less than the ref string. Try to remove every character from ref and see if the strings match. O(n^2) time O(n^2) space
if check string greater than ref string Try to remove every character from check and see if the strings match O(n^2) time O(n^2) space
if they are equal, check if theres more than one mismatch O(n) time O(1) space

## Optimize

the mismatch seems pretty clean as is for the replace operation.
For the length mismatch much can be improved. 

We can build a character indexed array first looping through the reference string and tallying the results
On the second run we can subtract for each character. 
if there is only a +1 or -1 in the array this is successful. 

This is O(n) or O(m+n) time, O(m+n) space

## Walk Through

if the length difference is greater than 1 return false
if the lengths are equal, loop through the first string and count the mismatches. If there is less than or equal to 1 mismatch at the end return true else return false
if the length differences are not equal, build a character indexed hashmap. Increment the tally for the ref string. Decrement for the check string.
loop through the tally array and check if theres more than one +/- 1 tally

## Implement

'''
bool OneAway(char[] reference, char[] check)
{
    if(Math.Abs(reference.Length - check.Length) > 1) return false;
    else if(reference.Length == check.Length)
    {
        bool misMatchFound = false;
        for(int i = 0; i < reference.Length; i++)
        {
            if(reference[i] != check[i])
            {
                if(misMatchFound) return false;
                misMatchFound = true;
            }
        }
        return true;
    }
    else 
    {
        Dictionary<char,int> tallies = new Dictionary<char,int>();
        for(int j = 0; j < reference.Length; j++)
        {
            tallies[j] = tallies[j] + 1;
        }

        for(int k = 0; k < reference.Length; k++)
        {
            tallies[k] = tallies[k] - 1;
        }

        bool foundOneOff = false;
        foreach(int val in tallies.Values)
        {
            if(val != 0)
            {
                if(foundOneOff) return false;
                foundOneOff = true;
            }
        }
        return true;
    }

}
'''

## Test

I ran through the given examples out loud and they all appeared to succeed


## Notes
1. Made an assumption then didnt stick to it and caught it while solving
2. Hashmap was a lazy approach and wasnt necessary. Didnt need memory allocations\][8]
3. Only found one solution. Should note that you can loop simultaneously based on the length
4. 