#dp 
# Statement
You are given a **0-indexed** integer array `nums`. You have to partition the array into one or more **contiguous** subarrays.

We call a partition of the array **valid** if each of the obtained subarrays satisfies **one** of the following conditions:

1.  The subarray consists of **exactly** `2` equal elements. For example, the subarray `[2,2]` is good.
2.  The subarray consists of **exactly** `3` equal elements. For example, the subarray `[4,4,4]` is good.
3.  The subarray consists of **exactly** `3` consecutive increasing elements, that is, the difference between adjacent elements is `1`. For example, the subarray `[3,4,5]` is good, but the subarray `[1,3,5]` is not.

Return `true` _if the array has **at least** one valid partition_. Otherwise, return `false`

**Example 1:**

**Input:** nums = [4,4,4,5,6]
**Output:** true
**Explanation:** The array can be partitioned into the subarrays [4,4] and [4,5,6].
This partition is valid, so we return true.

**Example 2:**

**Input:** nums = [1,1,1,2]
**Output:** false
**Explanation:** There is no valid partition for this array.

**Constraints:**

-   `2 <= nums.length <= 105`
-   `1 <= nums[i] <= 106`
<hr/>
# Solution
**Brute force to memoization**
The valid subarrays always have a size of 2 or 3. So we only have to check those arrays.
Algo:
1. Check for array of size 2 for validity
2. If valid, recursively check for remaining portion of array for validity
3. Check for array of size 3 for validity
4. if valid, recursively check for remaining portion of array for validity
```cpp
class Solution {
    bool isValid(std::vector<int>& nums) {
        if (nums.size() == 2 && nums[0] == nums[1])
            return true;
        if (nums.size() == 3 && (nums[0] == nums[1] && nums[0] == nums[2] 
                                 || (nums[2] - nums[1] == 1 && nums[1] - nums[0] == 1)))
            return true;
        return false;
    }
    
    bool f(std::vector<int>& nums, int left, std::vector<int>& dp) {
        if (left >= nums.size())
            return true;
        // check 2 and remaining
        if (left + 2 > nums.size())
            return false;
        if (dp[left] != -1)
            return dp[left];
        std::vector<int> p1(nums.begin() + left, nums.begin() + left + 2);
        if (isValid(p1) && f(nums, left + 2, dp))
            return dp[left] = 1;
        
        // check 3 and remaining
        if (left + 3 > nums.size())
            return false;
        std::vector<int> p2(nums.begin() + left, nums.begin() + left + 3);
        if (isValid(p2) && f(nums, left + 3, dp))
            return dp[left] = 1;
        
        return dp[left] = 0;
    }
    
public:
    bool validPartition(vector<int>& nums) {
        std::vector<int> dp(nums.size(), -1);
        return f(nums, 0, dp);
    }
};
```
- Time: `O(N)`
- Space: `O(N)`