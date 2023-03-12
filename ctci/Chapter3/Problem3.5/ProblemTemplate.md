# Problem 3.5

## Problem statement

Write a program to sort a stack such that the smallest items are on the top. You can use an additional temporary stack but no other data structures. The stack supports push pop peek and isEmpty.

## Solution Attempt

### Listen
Use system.collection.stack
allowed to use an additional stack
smallest to largest? yes

## Examples

## Brute Force

one example would be to use 2 temp stacks where you could popping one stack onto another grabbing the greatest. However this breaks project requirements

## Optimize

We could do sort of a bubble sort where we use a variable to hold a value, then the next value on the stackToPop gets pushed onto the other stack

## Walk Through

two stacks, inStack and tempStack.

first iteration
    pop the instack to a local variable.
    while instack isnt empty
    if the local variable is greater, push that onto the tempstack. else push the other onto the temp stack.
    set a boolean to true if a swap happened
second iteration
    pop the tempstack to a local variable
    while tempstack isnt empty
        if the local variable is less than push that onto the in stack. else push the tempstack onto the in stack and pop the next onto the local stack

## Implement

'''
public Stack<T> SortStack(Stack<T> inStack)
{
    if(inStack.Peek() == null) return inStack;
    Stack<T> retStack;
    Stack<T> tempStack = new Stack<T>();
    bool stackUnsorted = true;
    while(stackUnsorted)
    {
        int test = inStack.Pop();
        if(inStack.Peek() == null) return inStack; //already sorted
        stackUnsorted = false;
        while(instack.Peek() != null)
        {

            if(test > inStack.Peek()) tempStack.Push(test);
            else
            {
                stackUnsorted = true;
                tempStack.Push(inStack.Pop());
                if(inStack.Peek() == null) 
                {
                    tempStack.Push(test);
                    break;
                }
            }
        }
        if(!stackUnsorted) return inStack;
        test = tempStack.Pop();
        while(tempStack.Peek() != null)
        {
            if(test < tempStack.Peek()) inStack.Push(test);
            else 
            {
                stackUnsorted = true;
                inStack.Push(tempStack.Pop());
                if(tempStack.Peek() == null)
                {
                    inStack.Push(test);
                    break;
                }
            }
        }

    }
}

'''

## Test


## Notes. 
My solution is also O(n^2) and O(n) space however the code is a lot less clean than the provided solution