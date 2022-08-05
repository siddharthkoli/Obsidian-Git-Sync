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
2. All the bits before and including the 1st set bit (1) from the right will be as is.
3. All the bits after the 1st set bit (1) from the right will be inverted.

So for any `a` which is an integral power of 2, only 1 bit is set in the entire representation.