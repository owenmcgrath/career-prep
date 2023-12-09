# Blind 75 solutions

## Sequences

### 1. [Two Sum](https://leetcode.com/problems/reverse-linked-list/) <span style = "color:green">Easy</span>
- ❌ Brute force O(n^2) time O(1) space -> iterate through in a nested loop to see if ```nums[i] == nums[j]```
- ✅ Best O(n) time O(n) space -> store previous iterations in a ```hashmap<value,index>``` check if ```target-nums[i]``` is in the hashmap. 

### 217. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) <span style = "color:green">Easy</span>
- ❌ Brute force O(n^2) time O(1) space -> iterate with nested loop and see if ```nums[i] == nums[j]```
- ➖ O(nlogn) time and O(1) space -> edits in place, sort the list then iterate to see if ```nums[i] == nums[i+1]```
- ✅ O(n) time O(n) space -> use an unordered_set. iterate through each value, check if val is in the set otherwise insert

### 121. [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) <span style = "color:green">Easy</span>
- ❌ Brute force O(n^2) time O(1) space -> iterate with nested loop keeping track of ```maxVal = max(maxVal, nums[j]-nums[i])```
- ✅ O(n) time O(1) space -> iterate keeping track of the min val ```minVal = min(minVal, prices[i])``` and max profit ```maxProf = max(maxProf, prices[i] - minVal)```

### 242. [Valid Anagram](https://leetcode.com/problems/valid-anagram/) <span style = "color:green">Easy</span>
- ❌ O(nlogn) time O(1) space -> in place, sort each string and compare the strings
- ➖ O(n) time O(n) space -> have a map of the count of each character. Iterate through each character of s, incrementing, iterate through each character of t decrementing, check if everything in the map is 0
- ✅ O(n) time O(1) space -> use an array indexed by 'a' counting instead of a map

### 20. [Valid Parenthesis](https://leetcode.com/problems/valid-parentheses/) <span style = "color:green">Easy</span>
- ❌ O(n) time O(n) space -> use a stack of characters to check if each closing bracket matches the opening bracket
- ✅ O(n) time O(1) space -> in place, use the string itself as a stack, tracking an index and updating the parameter

### 53. [Maximum SubArray](https://leetcode.com/problems/maximum-subarray/) <span style = "color:green">Easy</span>
- ❌ Brute Force O(n^2) time and O(1) space -> Check every possible subarray
- ✅ O(n) time and O(1) space -> Kadane's algorithm. Keep track of a current sum with ```currSum = max(nums[i], currSum + nums[i])```. Keep track of best sum with ```bestSum = max(bestSum, currSum)```

### 238. [Product of array except self](https://leetcode.com/problems/product-of-array-except-self/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^2) time and O(n) space -> nested four loop calculating every possible product ```prod *= nums[j]``` except when j==i
- ✅ Prefix Suffix O(n) time and O(1) space -> have a prod = 1. skip i=0, multiply ```result[i]*=prod; prod*=nums[i]```. then do the same thing in reverse. 

### 15. [3Sum](https://leetcode.com/problems/3sum/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^3) time -> generate every possible triplet and check the sum. 
- ➖ O(n^2) time and O(n) space -> Sort the list, and store a set of ```vector<int>```, using a high low approach. iterate through the list to get i. if sum is too little move left one. if sum is too high move right 1 else put i,low,high on the set
- ✅ O(n^2) time and O(1) space -> Don't use a set. sort and find a match as before, but skip through the matches by incrementing low while equal, and decrementing high while equal. Also incrementing i while equal

### 56. [Merge Intervals](https://leetcode.com/problems/merge-intervals/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(N^3) time -> Nested loop through each pair of intervals and combine if necessary. Repeat until fixed.
- ✅ O(nlogn) time -> Sort the intervals by the first index. then iterate through each interval. merge overlaps by storing the min of the first value and the max of the end value. if theres no overlap just push it on the result.

### 49. [Group Anagrams](https://leetcode.com/problems/group-anagrams/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(kn^2) time -> keep a running list of groups perform the count comparison for each word against each group and push it on that group should it exist, otherwise make a new group
- ✅ O(nklog(k)) time O(n) space. Sort a copy of the strings use a ```unordered_map<string, vector<string>>``` and push the original string on the map value with the key being the sorted string. 

### 50. [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^2) time -> calculate the product for every possible subarray and find the maximum
- ➖ O(n) time 2 passes -> Kadane's algorithm prefix suffix. Find the max product iterating forward. If the product is zero reset the product to 1. Do the same in reverse. 
- ✅ O(n) time 1 pass -> Kadane's but hold the minimum and maximum values. When ```nums[i] < 0``` swap max and min. 

### 51. [Search in a Sorted Subarray](https://leetcode.com/problems/search-in-rotated-sorted-array/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n) time -> rotate the subarray back into place and then binary search. 
- ➖ O(log(n)) time two searches -> binary search the minimum value. 
- ✅ O(log(n)) time -> either the left or right half will be sorted. so theres 4 conditions. in sorted left half, in sorted right half, in unsorted left half, in unsorted right half. if its in the unsorted half, then you are doing the same thing on a smaller array. 

## Data Structures 
### 1. [Reverse a linked list](https://leetcode.com/problems/reverse-linked-list/) <span style = "color:green">Easy</span>
- ❌ Brute force O(n^2) time O(1) space -> Find the length of the linked list. get the last value iterate to the one before, set last_value->next to the one you iterated to. set last_value to this
- ✅ Best O(n) time O(1) space -> swap in 1 pass. prev = nullptr, it = head. while it not null: temp = it->next, it->next = prev, prev = it, it = temp; return it

### 141. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) <span style = "color:green">Easy</span>
- ❌ Brute force O(n) time O(n) space -> use an ```unordered_set<ListNode*>``` and check if a listnode has already been inserted
- ✅ Best O(n) time O(1) space -> use a slow and fast iterator. slow iterates once, fast iterates twice. when they meet there is a cycle.

### 11. [Container with Most Water](https://leetcode.com/problems/container-with-most-water/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^2) time -> calculate every possible length 2 subarray with their indices and compare the areas. 
- ✅ O(n) time -> Dynamic Window: high - low. compare low and high, move the ```height[i]``` which is less than the other. 

### 153. [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n) time -> loop through and find the minimum
- ✅ O(log(n)) time -> Binary Search. if ```nums[low] < nums[high]``` return nums low. if mids greater than low, look to the right, else look to the left

### 424. [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O((n+1)!) for every possible character replace each and calculate the longest substring of each character.
- ➖ O(n) time 26*n worst case-> Intuition. for each unique character in s, keep track of a repeating character start index, and the number of replacements used. if you run out of replacements, move the start index.
- ✅ O(n) time single pass -> iterate the counter of each character each time you pass, get the maximum and store in a vector. if the current window is greater than k, decrement the character count and move the start over 1.

### 3. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^2) loop through the characters, check if previous characters match current character
- ✅ O(n) time O(1) space single pass -> with an array of ints, indexed by character, keep an index of the last time you came across that character. if you reach that character again reference a new start to be one after the previous character index. keep a maxLen with i and start.

### 200. [Number of Islands](https://leetcode.com/problems/number-of-islands/description/) <span style = "color:yellow">Medium</span>
- ❌ Brute Force O(n^2) loop through the characters, check if previous characters match current character
- ✅ O(n) time O(1) space single pass -> with an array of ints, indexed by character, keep an index of the last time you came across that character. if you reach that character again reference a new start to be one after the previous character index. keep a maxLen with i and start.
