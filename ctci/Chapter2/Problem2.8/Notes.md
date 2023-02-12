# Problem 2.8

## Problem statement
Given a linked list which might contain a loop, implement an algorithm that returns the node at the beginning of the loop.

## Solution Attempt

### Listen
Return null if none exists? yes.
Handle empty lists?

## Examples

a -> b -> c -> d -> e -> c (same c) loop 3 4 it
a a
b c
c e
d d

a -> b -> c -> d -> c loop 2 3it
a a
b c
c c

a->b->c-> loop 1 3 it
a a
b c 
c c

a -> b -> c -> d -> e -> f -> c (same c) loop 4, 5 it
a a
b c
c e
d c
e e

a -> b -> c -> d -> e -> f -> g -> c (same c) loop 5, 6 it
a a
b c
c e
d g
e d
f f

re written for visual
        <-f
a->b->c     ->e
        ->d

## Brute Force

we could use a hashset of linkedlistnodes, if it contains the node return true. if we hit a null point return false
This is O(n) time and O(n) space

## Optimize

We don't have to use space with the two pointer technique. We could have a fast pointer and a slow pointer. One iterating once, another iterating twice. Eventually this will catch up. This is O(n) time and O(1) space.

The above is incorrect as this may not find the intersection. This is similar to finding a duplicate in a linked list. 

we can expand upon the two pointer solution. If we find a match we know there is a loop.
Once we are at the loop, we have found a loop of fixed length. We can reiterate the loop, and iterate around the loop for each iteration until we match the first iteration.

This is done in O(n^2) time and O(1) space

## Walk Through



## Implement

'''

'''

## Test


## Notes. 

Techniques to keep in mind when it comes to singly linked lists!!!
- Linked List reversal, handy for the palindrome problem.
- iterating both lists and at the end swapping. Useful for the intersection problem, or the string rotation problem before
- Slow pointer, fast pointer. For finding duplicates and cycle

Didnt find the pattern here.