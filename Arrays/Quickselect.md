```cpp
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
```
- Time: `avg: O(N), worst: O(N ^ 2)`
- Space: `O(1) [excluding recursion]`