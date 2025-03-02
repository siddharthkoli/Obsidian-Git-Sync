2 methods:
### Method 1: `O(N * LogN)` time
The idea is to keep a `map` or `multiset` that has all the items that are in the current window. the max element will always be at the end.
Using a `map` is straighforward by reducing the freq count.
If using a `multiset`, `multiset.erase()` will erase all occurrences of that element. So acquire a pointer to that element and then erase that.

### Method 2: `O(N)` time `O(K)` space
The idea is to use a ***monotonic*** `deque` to keep of the elements in the window. Since it is monotonic, the max element will be at the `front` of the `deque`. 