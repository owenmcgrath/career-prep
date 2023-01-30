# Technical Questions

## How to Prepare
1. Try to solve the problem on your own
2. Write the code on paper
3. Test the code on paper
4. Type code on paper as is into your computer

## What you need to know
| Data Structures | Algorithms | Concepts |
|-----------------|------------|--------- |
| Linked Lists | Breadth First Search | Bit Manipulation |
| Trees Tries & Graphs | Depth First Search | Memory (Stack vs Heap) |
| Stacks & Queues | Binary Search | Recursion |  
| Heaps | Merge Sort | Dynamic Programming | 
| Vectors/ArrayLists | Quick Sort | Big O Time & Space |
| Hash Tables | | | 

## Power of 2 Table
- Power of two table can be useful to have memorized. 
- I think this is unnecessary personally. Just know binary conversions 2^8
- It suggests having this available for web companies

## Walking through a problem
1. LISTEN
    - Pay close attention to all problem details
2. EXAMPLE 
    - Debug example, is it a special case? is it big enough?
3. BRUTE FORCE
    - Get a brute force solution done asap.
4. OPTIMIZE
    - Look for unused info from the problem statement
    - Solve manually on an example and reverse engineer it
    - Solve "incorrectly" then think about why the algorithm fails
    - Make a time v space tradeoff 
5. WALK THROUGH
    - Walk through the approach in detail
6. WRITE THE CODE
7. TEST 
    1. Conceptual test (code review)
    2. Unusual or non-standard code
    3. Hot Spots (math or null checking)
    4. Small Test Cases (faster than big test case and as effective)
    5. Special cases and edge cases
    6. Fix bugs carefully!

### What to expect
- Listen to the interviewer! They may/may not provide guidance

### 1. Listen Carefully
- Mentally record any unique info from the problem
  - i.e. "Given two arrays that are sorted" NOTE that they are sorted, this will change alg significantly
  - i.e. "Design alg to run repeatedly on server" NOTE repeated might need to signify caching? 
- Write info on the whiteboard

### 2. Draw example
Create an example that
- Is specific, use real numbers or strings
- Sufficiently large. Most examples are too small
- Not a special case. 

### 3. State a Brute Force Example
It can be a valuable discussion even though its a bad solution

### 4. Optimize
1. Look for unused info. (from step 1) 
2. Use a fresh example
3. Solve incorrectly.
4. Time v Space tradeoff. Sometimes using space helps time
5. Precompute info. Can you sort to save time?
6. Think about best possible runtime

### 5. Walk Through
- Pseudo code might be helpful but be wary if the pseudo code is too specific, its probably better to just write

### 6. Implement
- Start at top left corner
- avoid line creep
- Write beautiful code by modularizing
- Put template functions that do repetitive work. fill it in later if asked
- error checks
- Use other classes/structs if appropriate. Pretend the objects exist
- Use good variable names. Short & descriptive

### 7. Test
Testing with previously defined examples can take a long time. Do this instead:
1. Start with a conceptual test.
2. If the code looks weird try to justify it, if you cant fix it
3. double check null cases, integer division, iteration breaks. "hot spots"
4. Small & specific test case 
5. Special test case

## Optimize & Solve Technique 1 Look for BUD
BUD - Bottlenecks, Unnecessary Work, Duplicated Work
- The bottleneck is the most expensive piece of the algorithm. Try to optimize that first. 
- Repeated work, i.e. repeated searching could be reduced from O(n) to O(log n) or O(1) 

### Bottleneck
Example: count the pairs of integers in an array that sum up to k
1. Brute force solution starts with the first element, loops through the rest, then second element etc...
2. The bottleneck is the repeated searching
3. Sorting the array reduces the repeated search. O(n^2) to O(nlog(n))
4. Now sorting is the new bottleneck. 
5. How can you find things quickly in an unsorted array? Hashtable
6. Put everything in a hashtable and check if x+k or x-k exists in the hashtable. Algorithm is O(n)

### Unnecessary Work
Example: Print all solutions in a^3 + b^3 = c^3 + d^3 where abcd are integers between 1 and 1000
1. Brute force solution is a 4x nested loop and checking if the equation works
2. Its unnecessary to check for further solutions for d after getting a solution. So break!
3. Algorithm is still O(n^4), but can solve for d once having a,b,c. Itll round to an integer, check if it fits into eq!
4. Alg reduced to O(n^3)

### Duplicated Work
Using example from above
1. calculating ab pairs and cd pairs are repetitive. we should cache all pairs
2. Build hash map with all possible c^3 + d^3 as key, list of c,d pair as value
3. Then check with all a,b pairs
4. Can optimize again! we already have all a,b pairs in the map as c,d pairs.
5. loop through the hashmap, loop through each value in the list, then check if the equation is valid
6. Runtime is now O(n^2)

## Optimize & Solve Technique 2 DIY
Try to work through it intuitively. Computer science language sometimes freeze us up but we would naturally solve it if doing manually.
Example: Given small string s and big string b, find all permutations of small string in big string
1. The brute force solution of generating all permutations of s and searching in b is O(S! * B) (lengths)
2. Solve by hand and figure out how you did it!
3. "Sliding Window", move window of 4 characters along B and check if its within S

"reverse engineer" natural approach

## Optimize and Solve Technique 3 (Simplify and Generalize)
Simplify/tweak some constraint, then solve simplified version
Example: Check if a string can be made from characters of another string
1. Cut characters instead of whole words!
2. Build a hashmap with each character and their counts.
3. Decrement the hashmap looping through the string to check!

## Optimize and Solve Technique 4 (Best Case & Build)
Solve best case, then get worse and worse with examples
Example: Build all permutations of a string, assume all chars are unique
Test string "abcdefg"
"a" -> {"a"}
"ab" -> {"ab", "ba"}
"abc" -> {"abc", "acb", "cab", "bac", "bca", "cba"}
Recursive algorithm, insert new character into every position of the list and add to it

## Optimize and Solve Technique 5 (Data Structure Brainstorm)
Run through a list of data structures and try to apply each one (hacky)
Example: Random numbers and stored in a list, keep track of median
1. Linked List? No bad for sorting and searching
2. Array? maybe. Would be expensive for sorting  
3. Binary Tree? Possible as it naturally sorts itself. Median might be the top, but might also be average of middle two elements
4. Heap? Could have two heaps, one with big half with a min heap one with small half with a max heap

## Best Conceivable Runtime
Determining best possible run time can be a good way to determine the best solution
i.e. two arrays best case would be O(a + b)
i.e. Printing pairs in an array would be O(n^2)
- Example: Given two sorted arrays find the number of elements in common
- Best case is O(n) need to check each element in each array at least once. 
- Worst case is O(n^2) nested loop.
- Optimal is somewhere inbetween that.
- Most likely optimal is O(n) or O(nlog(n))
- This can be a good hint for what step to optimize
- One N comes from searching. The arrays are sorted! so the second search can become log(N)
- Now the algorithm is O(nlogn). Can it be done better? like O(log(n)) or O(1) ? 
- No! BCR is O(n). We cant reduce the N, we have to loop through the array at least once. Can we improve log(n)? Maybe!
- Since we already have O(n), we can just throw everything in a hash map, then we have O(1)!
- Now we've reduced to O(n) which is best case! nice!
- Can it be better? Well.... Our runtime is the same sorted or not.... We are in O(n) space lets go for O(1) space
- BST will work without memory allocation. Brute force with BST leads to O(nlog(n)). But whats the bottleneck? 
- We dont have to BST the whole list everytime. We can start with the last found index, as the next value cant be before that.
- Now we are approaching O(n) and O(1) space
 
## Handling Incorrect Answers
- Interviews are never flawless. Mistakes happen.
- Its not a binary outcome. "right wrong" doesnt matter as much. 

## When you have heard a question before
- Tell them. You arent giving them the opportunity to evaluate you properly

## The perfect language for interviews
- More widely known languages are better
- language readability helps
- Careful of extra bugs to worry about. i.e. pointer issues in C++
- Verbosity. Python takes less characters than java for example.
- Ease of use can be an advantage. Pythons easier than c++

## What good coding looks like
Good Code is ....
- Correct: Return all expected outputs from inputs
- Efficient: Be most time & space optimal, including real life circumstances
- Simple: Less lines is better!
- Readable: Well commented and designed to be understood
- Maintainable: Should be reasonably adaptable to changes in software lifecycle

### Use Data Structures Generously
i.e. write a function to add two math expressions like Ax^a + Bx^b
- Bad implementation defines the function input as an array of doubles. It would not be able to support negative values or would sometimes waste a lot of space
- Less Bad: splitting up into two arrays, coefficients and exponents. Would need to return multiple arrays
- Good implementation. Define a struct/class with coeff and exp and put in two summed arrays

### Appropriate Code reuse
- Split generic-ish functions into separate modular functions
- Modular code is easier to test!

### Flexible and Robust
- i.e. to check for a winner on tictactoe board. Dont assume 3x3, use nxn!

### Error checking
- Do asserts, error checking catch exceptions etc.
- Don't actually write the checks just explain that you would add them

## Don't Give Up! 
- Rise to the challenge and be excited about it!



