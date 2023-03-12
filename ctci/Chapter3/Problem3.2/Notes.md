# Problem 3.2

## Problem statement

How would you design a stack which in addition to push and poop has a function min which returns the minimum element?
Push, Pop, and min should all operate in O(1) time. 

## Solution Attempt

### Listen

Can this stack be dynamically allocated? Use stack node design.
What data type are we using? (integer)

## Examples

skipping because obvious

## Brute Force

(neglecting the O(1)) runtime requirement, You could use a stack along side a list of stack nodes that you sort on every push
and delete on every pop. This makes push (o(log(n))) and pop O(n) and min O(1)

This can be simplified to simply having 2 stacks. One that holds every element, another that holds minimums. 

I.e. for push. if the value to add is less than or equal to the value on the min stack, push it on the min stack and the full stack
Else push it only on the full stack.

for pop, pop the value on the full stack. if its equal to the peeked value on the min stack, pop the min stack.

min is just a peek on the min stack.

## Optimize

This solution is O(n) space and O(1) time for push peek and pop as asked for. The StackMin itself cant be constant space 
since its a collection. But the individual functions on the min stack are constant space.

## Walk Through

(above)

## Implement

'''

public class MinStack<T>
{
    private Stack<T> m_stack;

    private Stack<T> m_min;

    public MinStack<T>()
    {
        m_stack = new Stack<T>();
        m_min = new Stack<T>();
    }

    void Push(T item)
    {
        T min = m_min.Peek();
        if(min == null) m_min.Push(item);
        else if(item <= min) m_min.Push(item);
        m_stack.Push(item);
    }

    T Pop()
    {
        if(m_stack.Peek() == null) return null;
        if(m_min.Peek() == m_stack.Peek()) m_min.Pop();
        return m_stack.Pop();
    }

    T Min()
    {
        return m_min.Peek();
    }

}

'''

## Test


## Notes. 