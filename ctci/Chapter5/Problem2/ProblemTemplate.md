# Problem 5.2

## Problem statement

Binary to String. Given a real number between 0 and 1 (e.g. 0.72) that is passed in as a double, print the binary representation. If the number cant be accurately represented with at most 32 characters print error. 


## Solution Attempt

### Listen

How does binary look in a double format? 
each digit is raised to the second power, just like 10s for decimal.

Should I print a leading zero and decimal? yes. 
Leading zero's ? no.

## Examples
0.75 -> 0.11
0.625 -> 0.101
0.77777777777777 -> "ERROR"

## Brute Force
first boundary check. must be less than 1 and greater than 0.
initialize a sum to be the input 
initializa a fraction to be .5
initialize a stringbuilder. 
if the fraction is less than the sum, append a 1, subtract the fraction from the sum.
else append a 0.
divide the fraction by 2. 
if the sum is zero, print the stringbuilder and return. 

if we get to 30 print error.

This runs in O(n) time and O(1)space

## Optimize
Can this be done in O(1) time? I dont think so. Maybe there is some arithmetic sequence math trick that can do this though. 

We could make a marginal improvement by writing each character 1by1 and not using a stringbuilder. But this would just shift the overhead. 
I think stringbuilder makes the most sense here. 

## Walk Through
(above)

## Implement

'''
void BinaryToString(double val)
{
    if(val >= 1 || val <= 0) Console.WriteLine("ERROR");
    StringBuilder str = new StringBuilder(32);
    str.append('0');
    str.append('.');
    double sum = val;
    double fraction = 0.5;
    for(int i = 0; i < 30; i++)
    {
        if(sum >= fraction)
        {
            str.append('1');
            sum -= fraction; 
        }
        else 
        {
            str.append('0');
        }

        if(sum == 0)
        {
            Console.WriteLine(str.ToString());
            return;
        }
        
        fraction /= 2;
    }
    Console.WriteLine("ERROR");
    return;
}
'''

## Test


## Notes. 