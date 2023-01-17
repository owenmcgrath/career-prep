# Big O
## An Analogy
## Time Complexity 
- Types of runtimes are O(log N), O(N log N), O(N), O(N<sup>2</sup>), O(2<sup>n</sup>)
- You can have multiple variables. i.e. painting a fence thats w meters wide and h meters high is O(wh)

## Best Case, Worst Case, Expected Case
- Quick sort example. Pick a random element as a pivot, swaps values less than to the left, greater then to the right.
- Then sorts the left and right of the pivots recursively
1. BEST CASE
    - My guess is Everything is already sorted, and its O(n)
    - Guess is correct
2. WORST CASE
    - My guess is its O(log(n)) as it does tree-esque recursion on an oppositely sorted list
    - Incorrect, worst case is that the largest value is the pivot and the first value. O(n<sup>2</sup>)
3. AVERAGE CASE
    - My guess is somewhere between O(log(n)) and O(n)
    - Since I was originally incorrect the halfway point between O(n) and O(n<sup>2</sup>), the result is O(nlog(n))
- Best case is a useless metric.
- Worst case is generally the same as average case

## Space Complexity
- Memory usage also matters
- Array length is generally the space. For recursion this could be a call stack length
- Looping while calling a function does not increase stack length

## Drop the Constants
- Constants are not necessary

## Drop nondominant terms
- O(n<sup>2</sup> + n) -> O(n<sup>2</sup>)
- O(n + log(n)) -> O(n)
- O(5*2<sup>n</sup> + 1000N<sup>100</sup>) -> O(2<sup>n</sup>)
- General list from slowest to fastest O(n!), O(2<sup>n</sup>), O(n<sup>2</sup>), O(nlogn), O(n), O(log(n))

## Multipart algorithm, Add and Multiply
- nesting implies multiplication, sequential loops are additions O(mn) vs O(m+n)

## Amortized Time
- Allows description of time when things happen rarely (like array list allocation)

## log(n) runtimes
- binary search trees are an example
- Generally log(n) when halving list each iteration

## Recursive runtimes
- Provides an example where there is a sum of two recursive calls. 
- that makes a tree, which makes a O(2<sup>n</sup>)
- Space complexity is O(n). The deepest stack goes 5,4,3,2,1

## Problems

### Example 1
- The algorithm loops through the array twice generating a sum and a product. O(2n) becomes O(n)

### Example 2
- The algorithm nested loops each element in a single array. This is O(<sup>2</sup>)

### Example 3
- The second nest starts at the index of the first nest plus one. This creates half of a square. Still O(<sup>2</sup>)
- The formula is n(n-1)/2

### Example 4
- There is a nested loop through two separate arrays. This is O(mn)

### Example 5
- The same as above, nested array through two arrays, but there is also a third array that loops through 10000 times.
- Still O(mn) This would just add a multiplied third constant

### Example 6
- This is an algorithm to reverse an array. It loops through half of it. It is O(n), drop the 1/2 constant

### Example 7
- Gives a bunch of Big O Notation and asks whats equivalent to O(n)
- O(n + p) where p < n/2. This is equivalent to O(n). O(n + n/2) = O(n), drop constant
- O(2n) This is equivalent. O(2n) -> O(n), drop constant
- O(N + log(n)) This is equivalent. Drop the non-dominate term log(n)
- O(N + M) Not equivalent. Cannot reduce a multipart algorithm

### Example 8
- Suppose theres an algorithm that took an array of strings, sorted the string, then sorted the array. Whats the runtime?
- I believe this is O(m*n). Each string can be of different length, m is the length of the array, n is the max string len
- Incorrect. Sorting is O(nlog(n)). The string length is diff each time. let array len be m. 
- Sorting string is O(slog(s)). Indexing array is O(m). Sorting array is O(mlog(m)) Comparing string is O(s)
- O(s*mlog(m) + m*(slog(s))) = O(sm * (log(m) + log(s)))

### Example 9
- Summing values in a binary search tree recursively.
- My answer is that it traverses the whole tree, so it must be O(2<sup>n</sup>>)
- Incorrect. There are n nodes in the tree, it traverses N nodes, O(N)

### Example 10
- This checks if a number is prime by iterating from 2 to the sqrt of a number
- My guess was O(sqrt(n)). Which is correct. 

### Example 11
- This calculates factorial recursively
- Time Complexity is O(n)

### Example 12 
- prints all string permutations
- Permutation is all possible orderings of a string
- It loops through the whole string, splits the string and loops through each
- I was lost on this problem. Permutations are factorial. This is n*n*n!, so this is O(n!)
### Example 13
- Calculates fibonacci numbers
- This is a sum of recursive functions, this eventually becomes O(2<sup>n</sup>)

### Example 14
- Loops 0 to N and runs the fib algorithm which each. This is O(2^n)

### Example 15. 
- Like the previous it loops from 0 to n and caches the fibonacci sequence. The question states it has already run 
- This is O(n) when the fib function has ran because it has cached

### Example 16
- This recursively calculates the powers of 2 from 1 to n inclusive
- This is O(log(n))

## Additional Problems
### VI.1
- this algorithm uses a loop to multiply b * a. (weird)
- runtime is O(n)

### VI.2
- Code computes a<sup>b</sup> with recursively calculating the power below it
- O(b) runtime

### VI.3
- Does modular arithmetic with subtraction,division,multiplication
- No looping, its O(1)

### VI.4
- Calculates integer division with a while loop
- I think you can say this is done in O(b/a) time. idk if thats possible. Maybe its just O(ab)
- Incorrect its O(a/b)

### VI.5
- Calculates a square root by searching a binary search tree. O(log(n))

### VI.6 
- Another sqrt problem, this time by looping through each perfect square and checking if its equal. O(log(n))
- Incorrect O(sqrt(n)). Common sense it stops at the squareroot of the number

### VI.7
- An unbalanced BST takes O(log(n)) time to traverse. N being the number of nodes in the tree.
- Incorrect. The worst case tree would be just 1 long trunk, then it would be O(n)

### VI.8
- If the tree is not a BST, searching a value worst case would be O(n)

### VI.9 
- This function copies an array by looping through each value, copying each individual value up to that index every step
- Then it adds a new one.
- This is O(n<sup>2</sup>)

### VI.10
- This function calculates the number of digits in a number. O(log10(n))

### VI.11
- It loops through each character of the alphabet 26. Then does a factorial operation on all inbetween characters.
- O(n!)

### VI.12
- Mergesort on b O(blog(b))
- does binary search on each element in a on b O(alog(b))
- so this is (log(b)(a+b)) 