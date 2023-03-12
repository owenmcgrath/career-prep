# Problem 3.1

## Problem statement
Three in one. Describe how you would use a single array to implement three stacks

## Solution Attempt

### Listen
- Are the stacks of all the same data type? 
- Is the requirement of "only one array" basically no use of extra space than an allocated array?

N/A

## Brute Force
One thought is to keep an index for each stack that is tracked in the array, one that indexes up from the beginning, one that indexes down from the end and another that stays inbetween. 

The issue is the middle sort of floats and requires moving the middle stack every iteration. You lose the benefits of the stack O(1) push runtime as you have to move the middle stack's memory everytime you do an insert on the first stack. so if stacks were a (front indexed),b (middle), c (end) push and pop from stack b would be O(a).

We could make it so that stack a uses even indices, stack b uses odd indices, and stack c iterates from the back. This may lead to strange stack overflows. Stack overflows might occur when they shouldn't because even indices have empty memory etc.

Whats better? worst case runtime of O(a) or leaving gaps in memory? Is there a solution to both?

(received hint about circular array)
we could treat the three stacks like a ring buffer. 

This means O(n) inserts/removes are acceptable and we should keep all the stacks/queues back to back in memory

A brute force method here would be to always shift everything else when there is an add or remove. However this doesn't really employ a ring buffer type data structure. there would never be a wraparound.

## Optimize

## Walk Through

Option A (O(1) time, inefficient space usage)
For these solutions we don't want to assume a data type for scalability so we should use template classes. So we can define it as MultiStack<T>. 
For this case, it also makes sense to design it to be scalable to n stacks.
Add remove should take parameters of the stack identifier (lets assume number)
We store an array of counters that tell us the size of each stack. 
We need functions for push, peek, pop, and isEmpty. 
We use modular arithmetic to track indices in the array for push pop, and store the length.

Option B (O(n) time inserts, efficient space usage)
This example becomes a lot more nuanced for more than 3 stacks so lets assume only three. 
Stack 1 inserts move all of stack 2 to the right, checking for a collision with stack 3.
Stack 1 removes move all of stack 2 to the left. Dont need to touch stack 3
Stack 2 inserts check for collision with stack 3
Stack 2 removes only decrement.
Stack 3 inserts check for collisions with stack 2.
Stack 3 removes only decrement (increment)


## Implement

'''
class MultiStackFast<T>
{
    private T[] m_array;

    private int[] m_indices;

    MultiStackFast<T>(int space, int numStacks)
    {
        Assert(numStacks > 0);
        Assert(space > 0)
        m_indices = new int[numStacks];
        m_array = new T[space];
    }

    bool IsEmpty(int stackId)
    {
        Assert(stackId < m_indices.Length);
        return m_array[stackId] == 0;
    }

    void Push(int stackId, T item)
    {
        Assert(stackId < m_indices.Length);
        Assert(m_array.Length / m_indices.Length > m_indices[stackId]);
        m_array[m_indices[stackId] * m_indices.Length + stackId] = item;
        m_indices[stackId]++;
    }

    T Pop(int stackId)
    {
        Assert(stackId < m_indices.Length);
        if(m_indices[stackId] == 0) return null;
        T retVal = m_array[m_indices[stackId] - 1];
        m_indices[stackId]--;
        return retVal;
    }

    T Peek(int stackId)
    {
        Assert(stackId < m_indices.Length);
        return m_array[m_indices[stackId]]
    }
}

class MultiStackSlow<T>
{
    private T[] m_array;

    private int m_aLength;

    private int m_bLength;

    private int m_cLength;

    MultiStackSlow<T>(int space)
    {
        m_array = new T[space];
    }

    bool AIsEmpty(){ return m_aLength > 0; }
    bool BIsEmpty(){ return m_bLength > 0; }
    bool CIsEmpty(){ return m_cLength > 0; }
    
    T APeek(){ return m_aLength > 0 ? m_array[m_aLength - 1] : null; }
    T BPeek(){ return m_bLength > 0 ? m_array[m_array.Length + m_bLength] : null; }
    T CPeek(){ return m_cLength > 0 ? m_array[m_aLength - m_cLength] : null; }

    int TotalLength() {return m_aLength + m_bLength + m_cLength; }
    bool IsFull() { return TotalLength() >= m_array.Length - 1; }

    bool APush(T item)
    {
        if(!IsFull())
        {
            //move b values 1 over.
            for(int i = m_aLength + m_bLength; i > m_aLength; i--)
            {
                m_array[i] = m_array[i - 1];
            }
            m_array[m_aLength] = T;
            m_aLength++;
            return true;
        }

        return false;
    }

    bool BPush(T item)
    {
        if(!IsFull())
        {
            m_array[m_aLength + m_bLength] = T;
            m_bLength++;
            return true;
        }
        return false;
    }

    bool CPush(T item)
    {
        if(!IsFull())
        {
            m_array[m_array.Length - m_cLength] = T;
            m_cLength++;
            return true;
        }

        return false;
    }

    T APop()
    {
        if(m_aLength > 0)
        {

            T retVal = APeek();

            for(int i = m_aLength; i < m_aLength + m_bLength; i++)
            {
                m_array[i - 1] = m_array[i];
            }

            return retVal;
        }

        return null;
    }

    T BPop()
    {
        if(m_bLength > 0)
        {
            
            T retVal = BPeek();
            m_bLength--;
            return retVal;
        }
        return null;
    }

    T CPop()
    {
        if(m_cLength > 0)
        {
            T retVal = CPeek();
            m_cLength--;
            return retVal;
        }

        return null
    }

}


'''

## Test


## Notes. 
- Questions was strange. 
- Had to google template class syntax
- Circular buffer is a rabbit hole, not a feasible answer for interview time, too complicated. My answer was honestly better and cleaner to write.

