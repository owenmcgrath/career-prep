# Problem 3.6

## Problem statement
An animal shelter holds only dogs and cats, thats operates on a FIFO basis.
People must adopt the "oldest" based on arrival time. They can select a dog or a cat 
Create data structures to maintain this system and implement operations enqueue, dequeueAny, dequeueDog and dequeueCat. You may use 
built in LinkedList

## Solution Attempt

### Listen

## Examples

## Brute Force

## Optimize

## Walk Through

The fastest way to do this is to create a linked list where we track only the beginning of the list and the end of the list as member variables. 
Enqueues + (any_ Dequeue) would then be only O(1) space and time operations. 

We could also have three linked lists one of dog, one of cat, and one of both. This uses double the memory but is still O(n), and 
dequeue dog and dequeue cat are O(1) while dequeue any is O(n).

I'll let you tell me as the designer of the problem the more context of the users. Are people really cool with just any animal very often? 
I think no. Theres usually a war of taste between dog people and cat people, pets are quite the investment. 



## Implement

'''

public class AnimalShelter
{
    public enum AnimalType
    {
        cat,
        dog
    }

    private LinkedListNode<AnimalType> m_nextUp;

    private LinkedListNode<AnimalType> m_lastInserted;

    public void Enqueue(AnimalType animal)
    {
        if(m_lastInserted != null)
        {
            m_lastInserted.Next = new LinkedListNode<AnimalType>(animal);
        }
        else 
        {
            m_lastInserted.Next = new LinkedListNode<AnimalType>(animal);
            m_lastInserted = m_lastInserted.Next;
            m_nextUp = m_lastInserted;
        }
    }

    public AnimalType Dequeue()
    {
        if(m_nextUp == null) return null;
        else 
        {
            m_nextUp = m_nextUp.Next;
            return m_nextUp.Value;
        }
    }

    public AnimalType Dequeue(AnimalType animal)
    {
        if(m_nextUp.Value == animal)
        {
            LinkedListNode<AnimalType> toReturn = m_nextUp;
            m_nextUp = m_nextUp.Next;
            return toRetrun.Value;
        } 

        LinkedListNode<AnimalType> animal = m_nextUp;
        while(animal.Next != null)
        {
            if(animal.Next.Value == animal)
            {
                LinkedListNode<AnimalType> toReturn = animal.Next;
                animal.Next = animal.Next.Next;
                return toReturn.Value;
            }
        }
    }
}

'''

## Test


## Notes. 