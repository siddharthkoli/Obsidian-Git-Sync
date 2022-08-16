#heaps
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
- Time: `O(N * logK)`
- Space: `O(K)`

# Approach 3: Quickselect
#### Kth from the back means (N - K)th from the front
#### Always express K in terms of index
```cpp
class Solution {
	int quickselect(std::vector<int>& nums, int left, int right, int k) {
        int pivot = nums[right];
        int currInd = left;
        for (int i = left; i < right; i++) { // not including right since that is the pivot
            if (nums[i] <= pivot) {
                std::swap(nums[i], nums[currInd]);
                currInd++; // increment currInd every time a swap is made
            }
        }
        std::swap(nums[currInd], nums[right]); // put pivot in correct position
        // at this point, pivot will be somewhere around middle
        // elements less than pivot are to its left (may not be sorted)
        // elements greater than pivot are to its right (may not be sorted)
        
        // nums[currInd] is the (currInd)th largest element
        if (currInd == k)
            return nums[currInd];
        else if (currInd < k)
            return quickselect(nums, currInd + 1, right, k);
        else
            return quickselect(nums, left, currInd - 1, k);
    }

public:
	int findKthLargest(vector<int>& nums, int k) {
		k = nums.size() - k; // since kth largest from back is n - k from front
		return this->quickselect(nums, 0, nums.size() - 1, k);
	}
}
```
- Time: Avg - `O(N)` Worst Case - `O(N ^ 2)`
- Space: `O(1)` excluding recursion