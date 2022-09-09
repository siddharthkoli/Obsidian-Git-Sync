#bitwise 
Consider `n`.
Highest power of 2 less than `n` is given by:
```cpp
// FOR INT VALUES
0x80000000 >> (__builtin_clz(n) - 1);
// 0x80000000 is INT_MAX + 1
// since above hex is stored as unsigned int, it does not overflow

// FOR LONG LONG VALUES
0x8000000000000000 >> (__builtin_clzll(n) - 1);
// 0x8000000000000000 is LONG_LONG_MAX + 1
```

### How does it work?
`0x80000000 (INT_MAX + 1)` is stored as `unsigned int`. That's why it does not overflow.
Its binary representation is `10000000 00000000 00000000 00000000` i.e. `1` followed by all `0`.

Refer: [Codeforces Article](https://codeforces.com/blog/entry/72437)