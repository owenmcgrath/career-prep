# Problem 1.9

## Problem statement
String Rotation: Assume you have a method isSubstring which checks if one word is a substring of another. Gven two strings
s1 and s2 write code to check if s2 is a rotation of s1 using only one call to issubstirng

## Solution Attempt

### Listen
Ascii or unicode? ASCII
null terminated? no, use str.
null or empty strings? no
can smaller strings be rotations? like sections? no

## Examples
s1: "waterbottle" s2: "erbottlewat" true
s2: "abcd" s2: "cbad": false

## Brute Force
Find a character from s1 that matches the first char of s2, iterate with two pointers through both,
if theres a mismatch reset the pointer for s2. If you reach the end of the string go to the beginning
If you have iterated more than the length of the strings, and you havent gotten n matches in a row then its not a rotation
if it is then its true. 

This is O(n) time O(1) space.

## Optimize

We haven't used substring yet. we can only use it once. Can we leverage this to be better?
Worst case we have to loop through the whole string twice. We could make it so that we only have to loop through once.
what if we looped through s2 until we reach a character that matches the first character of s2, then substring the rest of 
the string with s1. If so? check if 1 through that index then matches manually the rest of the string.

This still will worst case loop twice.

(after receiving hint)
conctenation will be O(n). Concatenate the string to itself then do an isSubstring.

## Walk Through

append s1 to itself then do s2.substring(). I think this is less efficient than the method i came up with previously but the problem is asking to use one call.


## Implement

'''
public bool StringRotation(string s1, string s2)
{
    s2 += s2;
    return isSubstring(s1, s2);
}

'''

## Test


## Notes. 
- Assumptions were different in the book but i 100% this with the hint.
- My solution was still more efficient. This was simpler to read even though it had more space used