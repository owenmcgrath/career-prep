# Problem 3.3

## Problem statement

SetOfStacks should be composed of several stacks and should create a new stack once the previous one exceeds capacity. 
push and pop should behave identically to a single stack.

FOLLOW UP
Implement a function popAt(int index) which performs a pop operation on a specific sub-stack.

## Solution Attempt

### Listen

What should we return if we try to pop an empty stack? 

## Examples

//not really applicable

## Brute Force

If it werent for the follow up, I would create a nested stack. (i.e. Stack<Stack<T>>)

Since there is the follow up where we need to reference smaller stacks by index it seems fitting that we use a List of stacks.

push will be O(1) time, with the occasional instantiation of a new stack at capacity.
pop will be O(1) time, just need to get the end of the list and pop off that stack, with occasional stack removal.
popAt will also be O(1) time. Reference the stack at that index and pop that stack.

## Optimize

public class SetOfStacks<T>
{
    private List<Stack<T>> m_set;

    private uint m_capacity;

    public SetOfStacks<T>(uint capacity)
    {
        m_set = new List<Stack<T>>();
    }

    public void Push(T item)
    {
        if(m_set[m_set.Count - 1].Count == (int)m_capacity)
        {
            m_set.Append(new Stack<T>());
        }

        m_set[m_set.Count-1].Push(item);
    }

    public T Pop()
    {
        if(m_set.Count == 0) return null;
        if(m_set[m_set.Count - 1].Count == 0)
        {
            m_set.RemoveAt(m_set.Count - 1);
        }

        if(m_set.Count > 0)
        {
            return m_set[m_set.Count - 1].Pop();
        }
    }

    public T PopAt(uint i)
    {
        if(i > (uint)m_set.Count) return null;
        T retVal =  m_set[i].Pop();

        Stack<T> tempStack = new Stack<T>();
        //now we gotta do the rollover
        for(int j = i + 1; j < m_set.Count; j++)
        {
            
            while(m_set[j].Peek()!= null) tempStack.Push(m_set[j].Pop());
            m_set[j - 1].Push(tempStack.Pop())
            while(tempStack.Peek() != null) m_set[j].Push(tempStack.Pop());
        }

        if(m_set[m_set.Count - 1].Peek() == null) m_set.RemoveAt(m_set.Count - 1);

        return retVal;
    }
}

## Walk Through


## Implement

'''

'''

## Test


## Notes. 
I should have known to ask about the rollover case for the follow up pop-at. I assumed it would just be fine if some inbetween
substacks operated not at full capacity. Would be easy to clear up with interviewer.