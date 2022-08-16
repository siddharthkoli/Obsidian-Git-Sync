# Approach 1: Sorting
```cpp
int findKthLargest(vector<int>& nums, int k) {
	std::sort(nums.begin(), nums.end());
	auto itr = nums.begin();
	int n = nums.size();
	std::advance(itr, n - k);
	return *itr;
}
```