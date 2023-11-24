# Algorithms and Computation
## Goals
1. Solve computational problems
2. Prove correctness
3. Argue efficiency
4. Communication of these ideas

## What is a problem
a space of inputs and a space of outputs.
A problem is a binary relationship between the inputs and outputs
looking for general problems with arbitrarily sized inputs. 

## What is an algorithm
a function that maps an input to an output
an algorithm solves a problem if it returns a correct output for every correct input. 

example: check if matching pairs of birthdays inthe class

interview each student
    if theres a record for that birthday return the pair of students
    else add a new student to the record
return none if all students interviewed without success

## Correctnes
Must use induction (proof that a mathematical law holds for all possible inputs k) and recursion

induct on k the number of students.
Inductive hypotheses:
    if first k contain match, returns the match before interviewing student k+1
Base Case: 
    k = 0 -> no students means no pairs
consider k = k' and k = k' + 1

if k' contains match, already returned a match
else first k' no match, so if k'+1 has a match match contains k'+1
Then algorithm checks directly whether birthday of student k'+1 exists in first k'

## Efficiency
How fast an algorithm runs
We want to create a metric for efficiency, but needs to be hardware independent. abstract it!
Don't measure time, count operations: Asymptotic analysis
expect to depend on the size of the input.
Variable is usually n

O(.) Upper bound Omega(.) lower bounds Theta(.) is both.

O(1), O(logn), O(n) O(nlogn) O(n^2) O(n^c)  < efficient

## Model of Computation
- Spec for what operation can be performed in O(1) time. 
- Called Word