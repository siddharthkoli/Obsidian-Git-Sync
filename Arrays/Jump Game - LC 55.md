#greedy
Assume a window starting from the current index and ending at the highest reachable index.
While iterating through the elements, if the current index falls within the window, its end can be extended.
The start of the window now becomes the current index.
While traversing, if you encounter an index which is outside the current window, then you cannot reach the end as you're trying to access an index outside the jumping range.
```cpp

```