#heaps
# Approach 1: Sorting
#### Always express K in terms of index
```cpp
int findKthSmallest(vector<int>& nums, int k) {
	std::sort(nums.begin(), nums.end());
	auto itr = nums.begin();
	int n = nums.size();
	k--;
	std::advance(itr, k); // express k in terms of index
	return *itr;
}
```
- Time: `O(N * log N)`
- Space: `O (1)`

# Approach 2: Max Heap
#### Use min heap for kth largest and max heap for kth smallest
```cpp
int findKthSmallest(vector<int>& nums, int k) {
	priority_queue<int> queue;
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
	int findKthSmallest(vector<int>& nums, int k) {
		k--;
		return this->quickselect(nums, 0, nums.size() - 1, k);
	}
}
```
- Time: Avg - `O(N)` Worst Case - `O(N ^ 2)`
- Space: `O(1)` excluding recursion