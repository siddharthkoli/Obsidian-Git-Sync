#dp #knapsack
The idea is to start from the end and for every index i, iterate over all the next elements till the end of array and find the lis
Since lis of a single element is always 1, the recurrence relation is 
`lis[i] = max(1, 1 + lis[j])`

Refer: [Neetcode](https://www.youtube.com/watch?v=cjWnW0hdF1Y)

code:
```cpp
class Solution {
    // returns length of lis ending starting at i
    int lis(std::vector<int>& nums, int i, std::vector<int>& dp) {
        int mx = 1;
        if (dp[i] != -1)
            return dp[i];
        for (int j = i + 1; j < nums.size(); j++) {
            if (nums[j] > nums[i])
                mx = std::max(mx, 1 + lis(nums, j, dp));
        }
        return dp[i] = mx;
    }
    
public:
    int lengthOfLIS(vector<int>& nums) {
        #if 0
        std::vector<int> dp(nums.size(), -1);
        int result = 1; // since a single element will always be an lis
        for (int i = nums.size() - 1; i >= 0; i--)
            result = std::max(result, lis(nums, i, dp));
        return result;
        #endif
        
        // time: O(N ^ 2)
        // space: O(N)
        #if 1
        std::vector<int> dp(nums.size(), 1);
        for (int i = nums.size() - 1; i >= 0; i--) 
            for (int j = i + 1; j < nums.size(); j++) 
                if (nums[i] < nums[j]) 
                    dp[i] = std::max(dp[i], 1 + dp[j]);
        return *std::max_element(dp.begin(), dp.end());
        #endif
    }
};
```

