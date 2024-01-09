#twopointers 
Use a hash map to keep count of total distinct elements in the current window.
The important trick to remember here is that between any `[start, end]`, as long as you have less than `k` distinct elements, keep increasing the window size.
Once there are more than `k` distinct elements, we can increment `res` with all the subarrays that start with `start` -> `[start, end], [start + 1, end], [start + 2, end] ... [end, end]`.
This is given by `end - start + 1`.
```cpp
int countSubarrays(std::vector<int>& nums, int k) {
	std::unordered_map<int, int> hash;
	int res = 0;
	int start = 0, end = 0;
	while (end < nums.size()) {
		hash[nums[end]]++;
		while (hash.size() > k) {
			hash[nums[start]]--;
			if (hash[nums[start]] == 0)
				hash.erase(nums[start]);
			start++;
		}
		res += end - start + 1;
		end++;
	}
	return res;
}
```