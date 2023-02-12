# Problem 1.4

## Problem statement
Palindrome Permutation: Given a string write a function to check if its a permutation of a palindrome. A palindrome is a 
word thats the same forwards and backwards. A permutation is a rearrangement of letters. It doesnt have to be dictionary words. 
You can ignore case and non-letter characters

## Solution Attempt

### Listen
have to handle case differences. (put a ToLower) in front of each character
Ignore the character if its a non letter. 
Can I have a ToLower function? No.
Are empty strings palindromes? Yes.
Are strings with 1 character palindromes? Yes.
Ignore nullable strings? Yes.

## Examples

"Tact Coa" -> true {taco cat, atco cta, etc}
"aa123cerrc" -> true {racecar, etc}

## Brute Force
if its empty return true
Remove all the non letters, and convert the uppercase to lowercase
Generate all the permutations with a list of strings and a nested for loop
Starting with the beginning of the string and the end of the string, while the indices are not equal, increment the first idx,
decrement the second index, check if the characters are equal. if they arent no permutation. If you get through a string and its a permutation return true

## Optimize

A palindrome must have pairs of characters minus 1 (if its an odd length)
A hashmap to track character counts could be generated, then checking if there is more than one odd count. (filtering non characters and changing upper to lowercase)
This won't require a hashmap. An array would use O(1) space. This would be O(n), O(1) space. 
We can't avoid the array allocation by using an unsigned integer, since we will have more than 1 to tally
Can we make this O(log(n)) ? Don't see how we can make this a singular binary search.

## Walk Through
Create a function to convert uppercase to lowercase. 
    check if the character is between 'A' and 'Z' inclusive, return char - 'A' + 'a'
    else return the char
Create a function to determine if the character is a letter
    check if its between 'A' and 'Z' inclusive or 'a' and 'z' inclusive

if the input length is less than or equal to 1 return true
initialize an array of length 'z' - 'a' + 1
loop through the input string and tally the character at that index
initialize a boolean to specify if an odd number has been reached.
loop through the array, if we have reached an odd number and the boolean is true return false.
if we get through the array return true


## Implement

'''
char ToLower(char c)
{
    if(c >= 'A' && c <= 'Z')
    {
        return (c-'A') + 'a';
    }
    return c;
}

bool IsLetter(char c)
{
    return (c >= 'A' && c <= 'Z') || (c <= 'z' && c >= 'a');
}

bool PalindromePermutation(string str)
{
    if(str.Length <= 1) return true;
    int[] tallies = new int['z'-'a' + 1];
    for(int i = 0; i < str.Length; i++)
    {
        if(IsLetter(str[i]))
        {
            tallies[ToLower(str[i])]++;
        }
    }

    bool reachedOdd = false;
    for(int i = 0; i < tallies.Length; i++)
    {
        if(tallies[i] % 2 > 0)
        {
            if(reachedOdd) return false;
            reachedOdd = true;
        }
    }

    return true;
    
}

'''

## Test
 
Can I assume ToLower and IsCharacter are correct? yeah!

"Tact Coa"
tallies: { a:2 c:2 t:2 }

"aa123cerrc"
tallies: {a:2 c:2 e:1 r:2 }


## Notes. 
1. Felt good about solving this one
2. The solution provides an alternative thats not necessarily faster that counts the odd numbers as you tally.
3. Didnt note how inefficient brute force was! O(n!)