# Sets and sorting
- Interface: collection of operations
- Data Structure: Way to store data that supports a set of operations

## Set interface
build(A) : given an iterable A build sequence from items in A | O(n)
len() : return the number of stored items 
find(k): return the stored item with key | O(n)
insert(x): add x to set (replace with key x.key if one already exists)
delete(x): remove and return the stored item with key k
iter_od(): return the stored items one by one in key order
find_min(): return the stored item with the smalllest key | O(n)
find_max(): return the stored item with the largest key | O(n)
find_next(k): return the stored item with smallest key larger than k | O(n)
find_prev(k): return the stored item with the largest key smaller than k | O(n)

if you wanted to do a sorted array:
build_a() takes nlogn
find() take logn
find_min O(1)

## Sorting
input is array of n numbers/keys a
output is a sorted array b

### Permutation Sort.
    check all permutations of an array
    find the vaidated permutation. 

BRUTE FORCE! 
generate permutations O(n!) time
check if its sorted 
    for i = 1 to n-1
        B[i] <= B[i+1]

This takes O(n! * n) time. 

### Selection Sort
8 2 4 9 3
find thebiggest number and swap it with the end
8 2 4 3 9
3 2 4 8 9
3 2 4 8 9
2 3 4 8 9

1. Found biggest with index <= 1
    ```
    /*
        1. It is at index I
        2. It isn't at index i
    */

    def prefix_max(A, i):
        if i > 0:
            j = prefix_max(A, i-1)
            if A[i] < A[j]
                return j
        return i
    ```
    inductive proof:
    base case i = 0

2. Swap
3. Sort 1, ... , i-1

### Merge Sort Example
7 1 5 6 2 4 9 3

take pairs and sort the box
[1 7] [5 6] [2 4] [3 9]

then merge half and half in sorted order
[1 5 6 7] [2 3 4 9]
[1 2 3 4 5 6 7 9]

two finger approach to merging sorted lists. 

This takes n logn time. 


