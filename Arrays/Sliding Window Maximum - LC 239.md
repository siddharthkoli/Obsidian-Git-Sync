2 methods:
### Method 1: N * LogN time

The idea is to keep a `map` or `multiset` that has all the items that are in the current window. the max element will always be at the end.
Using a `map` is straighforward by reducing the freq count.
If using a `multiset`, m