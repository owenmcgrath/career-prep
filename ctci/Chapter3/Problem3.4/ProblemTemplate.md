# Problem 3.4

## Problem statement
Queue via Stacks: Implement a MyQueue class which implements a queue using two stacks.

## Solution Attempt

### Listen
Implement with System.Collections.Stack ? yes.
Generic type.

## Examples

## Brute Force

When you iterate through a stack, pushing each element onto another stack. it essentially reverses the list every time.

This can help us access the oldest (since insert) item and push it and retrieve it. 

What if we were to have the Enqueue operation insert onto stack A. 
For the dequeue operation, if there is an item on stack B, pop and return. otherwise, push everything on stack A, onto stack B
then pop the last item off of stack b.

## Optimize

The occasional reversal seems to be inefficient. But I don't think theres a good way to avoid that. (that appears to be the case based on the hints)

## Walk Through

For push, just push onto the inStack. 
For pop, if the out stack is empty, if the in stack is empty return null pop everything off the instack onto the out stack, then pop the out stack
else pop the out stack


## Implement

'''

public class TwoStackQueue<T>
{
    Stack<T> m_inStack;

    Stack<T> m_outStack;

    public TwoStackQueue<T>()
    {
        m_inStack = new Stack<T>();
        m_outStack = new Stack<T>();
    }

    public void Enqueue(T item)
    {
        m_inStack.Push(item);
    }

    public T Dequeue()
    {
        if(m_outStack.Peek() == null)
        {
            while(m_inStack.Peek() != null) m_outStack.Push(m_inStack.Pop());
        }

        return m_outStack.Pop();
    }

    public void Enqueue(T item)
    {
        m_inStack.Push(item);
    }

    public T Peek()
    {
        return m_outStack.Peek();
    }
}

'''

## Test


## Notes. 