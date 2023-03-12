# Chapter 5 Bit Manipulation. 
## Bit manipulation by hand

| Equation | Answer | 
| -------- | ------ |
| 0110 + 0010 | 1000 | correct
| 0011 + 0010 | 0101 | correct
| 0110 - 0011 | 0010 | incorrect (careless error)
| 1000 - 0110 | 0010 | correct
| 0011 * 0101 | 1111 | correct
| 0011 * 0011 | 1001 | correct
| 1101 >> 2 | 0011 | correct
| 1101 ^ 0101 | 1000 | correct
| 0110 + 0110 | 1010 | incorrect 1100 (careless error)
| 0100 * 0011 | 1100 | correct
| 1101 ^ (~1101) | 1111 | correct
| 1011 & (~0 << 2) | 1000 | correct

Tricks:
0110 + 0110 is equal to 0110 * 2, which is the equivalent of a left shift by 1 bit.
0100 is 4, multiplying by 4 is left shifting 2. 
a^(~a) is always full 1's
ANDing a shifted full byte with another value is chopping off the last bits for the number you shifted by.

## Bit facts/tricks
Important ones
x^0s = x
x^1s = ~x exclusive or'ing with a full integer will just swap all bits, just like ~
x^x = 0s. all the bits match so no exclusive OR's
x & 0s = 0s. Cant ever have matching 1's if you are matching with 0
x & 1s = x. Only matches will be with set bits, value wont change
x & x = x. Only matching 1's will be with its own bits. 
x | 0s = x. If matching bits with 0, only true bits will be bits set on x
x | 1s = 1s All bits will be true when or'ing with 1.
x | x = x. Only true when bit from x is set, resulting in x

## Two's complement and negative numbers.
negative values have furthest left bit set and their positive implementation
~x + 1 makes x negative.

## Arithmetic vs logical right shift
Arithmetic right shift divides by two (shift then fill new bits with the sign bit)
logical right shift actually shifts the bit. (shift then fill the new bits with 0)

## Common bit tasks
### Get bit
shifts a bit by an amount then checks if its AND is not 0

```
bool GetBit(int val, int idx) 
{
    return (val & (1 << idx)) != 0;
}
```

### Set bit
OR's a bit at idx

```
int SetBit(int val, int idx)
{
    return (val | (1 << idx));
}

```

### Clear bit
Flips just that set bit and &'s it. 
```
int ClearBit(int val, int idx)
{
    return (val & ~(1 << idx));
}
```

```
int ClearMSBthroughIdx(int val, int idx)
{
    return (val & ((-1 << i) - 1));
}
```

```
int ClearBitsIdxThrough0 (int val, int idx)
{
    return val & ((1 << i) - 1);
}
```

clear the bit then set it. 
```
int UpdateBit(int num, int i, bool bit)
{
    int val = bit ? 1 : 0;
    int mask = ~(1 << i);
    return (num & mask) | (val << i);
}
```