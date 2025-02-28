The problem asks to return actual numbers and not their indices.
Also the triplets should not be repeated.

Sort and use 2 pointers, and skip repeated numbers.

```cpp
class Solution {
    // time: O(N)
    void findSum(std::vector<int>& nums, int target, int i, std::vector<std::vector<int>>& result) {
        int start = i + 1, end = nums.size() - 1;
        while (start < end) {
            int currSum = nums[start] + nums[end];
            if (currSum == target) {
                result.push_back({nums[i], nums[start], nums[end]});
                start++, end--;
                while (start < end && nums[start] == nums[start - 1]) start++;
                while (end > start && nums[end] == nums[end + 1]) end--;
            } else if (currSum > target)
                end--;
            else
                start++;
        }
    }
    
public:
    // time: O(N ^ 2) space: O(1) not counting result array
    vector<vector<int>> threeSum(vector<int>& nums) {
        if (nums.size() < 3)
            return std::vector<std::vector<int>>();
        // O(N * logN)
        std::sort(nums.begin(), nums.end());
        
        // O(N ^ 2)
        // this loop executes in O(N), findSum take O(N)
        // hence O(N ^ 2)
        std::vector<std::vector<int>> result;
        for (int i = 0; i < nums.size() - 2; i++) {
            if (i > 0 && nums[i] == nums[i-1])
                continue;
            findSum(nums, -nums[i], i, result);
        }
        return result;
    }
};
```
