# Hashing
## Comparison Model
Represent sorting algorithms as a decision tree, with leaves being the outputs of a comparison
the comparisons are = < > >= <= != 

The minimum height of the decision tree is average case logn

## Direct Access Array
Store an item with key 10 at index 10. 
Store and access in constant time O(1)

The problem is that you would have to way over-allocate the array to pull this off when there is a large amount of values. 
The example he used was a direct access array for the class of 9 digit MIT ID numbers

If you want to run in constant time, the size of the largest key must be less than 2^(word size) (32)

## Division hash function 
h(k) = k mod m

## Universal Hash function
hab(k) = (((ak +b) mod p) mod m)
which is described better as....
H(p,m) = {hab(k) | a,b choose {0,....,p-1}} and a != 0
