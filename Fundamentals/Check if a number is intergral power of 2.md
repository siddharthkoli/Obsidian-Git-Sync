#bitwise
Consider a number `a`, then check for: `a & -a == a`
Let's say `a` is 8: `0001000`
-8 is represented as 2's complement: `1111000`
So the check is:
```
	0001000
  & 1111000
  -----------
    0001000
```

Finding 2's complement is as follows:
1. Find the first 1 from the right of the binary representation.
2. All the bits to the right and including the 1st set bit (1) from the right will be as is.
3. All the bits to the left of the 1st set bit (1) from the right will be inverted.

How does it work?
For any `a` which is an integral power of 2, only 1 bit is set in the entire binary representation.
All bits to the right of set bit will be zero and not changed including the set bit.
All the bits to the left will be inverted.
So in the check, left bits will be 0, and right bits will remain as is.

For any `a` which is NOT an integral power of 2, more than 1 bits are set in the binary representation.
This changes the 2's complement and the check fails
eg.
```
	0001010
  & 1110110
  ----------
	0000010
```
