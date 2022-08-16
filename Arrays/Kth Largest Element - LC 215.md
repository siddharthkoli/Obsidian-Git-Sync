# Approach 1: Sorting
#### Kth from the back means (N - K)th from the front
#### Always express K in terms of index
```cpp
int findKthLargest(vector<int>& nums, int k) {
	std::sort(nums.begin(), nums.end());
	auto itr = nums.begin();
	int n = nums.size();
	std::advance(itr, n - k); // express k in terms of index
	return *itr;
}
```
- Time: `O(N * log N)`
- Space: `O (1)`

# Approach 2: Min Heap
#### Use min heap for kth largest and max heap for kth smallest
```cpp
int findKthLargest(vector<int>& nums, int k) {
	priority_queue<int, vector<int>, greater<int>> queue;
        for (auto x: nums) {
            queue.push(x);
            while (queue.size() > k)
                queue.pop();
        }
        return queue.top();
}
```
