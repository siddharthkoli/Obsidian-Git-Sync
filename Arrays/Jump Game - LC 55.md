#greedy
Assume a window starting from the current index and ending at the highest reachable index.
While iterating through the elements, if the current index falls within the window, its end can be extended by adding the current element to the start of the window (creates new window).
This new window size can be kept or dis
The start of the window now becomes the current index.
While traversing, if you encounter an index which is outside the current window, then you cannot reach the end as you're trying to access an index outside the jumping range.
```cpp
bool canJump(const std::vector<int>& nums) {
	int start = 0, end = 0;
	for (int i = 0; i < nums.size(); i++) {
		if (i > end)
			return false;
		start = i;
		end = std::max(end, start + )
	}
}
```