#dp #knapsack

# Greedy Approach
-   Let's construct the idea from following example.
-   Consider the example `nums = [2, 6, 8, 3, 4, 5, 1]`, let's try to build the increasing subsequences starting with an empty one: `sub1 = []`.
    1.  Let pick the first element, `sub1 = [2]`.
    2.  `6` is greater than previous number, `sub1 = [2, 6]`
    3.  `8` is greater than previous number, `sub1 = [2, 6, 8]`
    4.  `3` is less than previous number, we can't extend the subsequence `sub1`, but we must keep `3` because in the future there may have the longest subsequence start with `[2, 3]`, `sub1 = [2, 6, 8], sub2 = [2, 3]`.
    5.  With `4`, we can't extend `sub1`, but we can extend `sub2`, so `sub1 = [2, 6, 8], sub2 = [2, 3, 4]`.
    6.  With `5`, we can't extend `sub1`, but we can extend `sub2`, so `sub1 = [2, 6, 8], sub2 = [2, 3, 4, 5]`.
    7.  With `1`, we can't extend neighter `sub1` nor `sub2`, but we need to keep `1`, so `sub1 = [2, 6, 8], sub2 = [2, 3, 4, 5], sub3 = [1]`.
    8.  Finally, length of longest increase subsequence = `len(sub2)` = 4.
-   In the above steps, we need to keep different `sub` arrays (`sub1`, `sub2`..., `subk`) which causes poor performance. But we notice that we can just keep one `sub` array, when new number `x` is not greater than the last element of the subsequence `sub`, we do binary search to find the smallest element >= `x` in `sub`, and replace with number `x`.
-   Let's run that example `nums = [2, 6, 8, 3, 4, 5, 1]` again:
    1.  Let pick the first element, `sub = [2]`.
    2.  `6` is greater than previous number, `sub = [2, 6]`
    3.  `8` is greater than previous number, `sub = [2, 6, 8]`
    4.  `3` is less than previous number, so we can't extend the subsequence `sub`. We need to find the smallest number >= `3` in `sub`, it's `6`. Then we overwrite it, now `sub = [2, 3, 8]`.
    5.  `4` is less than previous number, so we can't extend the subsequence `sub`. We overwrite `8` by `4`, so `sub = [2, 3, 4]`.
    6.  `5` is greater than previous number, `sub = [2, 3, 4, 5]`.
    7.  `1` is less than previous number, so we can't extend the subsequence `sub`. We overwrite `2` by `1`, so `sub = [1, 3, 4, 5]`.
    8.  Finally, length of longest increase subsequence = `len(sub)` = 4.
![[Pasted image 20220731001958.png]]
```cpp
int lengthOfLIS(vector<int>& nums) {
	std::vector<int> sub;
	sub.push_back(nums[0]);
	for (int i = 1; i < nums.size(); i++) {
		if (nums[i] > sub[sub.size() - 1])
			sub.push_back(nums[i]);
		else {
			auto itr = std::lower_bound(sub.begin(), sub.end(), nums[i]);
			*itr = nums[i];
		}
	}
	return sub.size();
}
```
-   Time: `O(N * logN)`, where `N <= 2500` is the number of elements in array `nums`.
-   Space: `O(N)`, we can achieve `O(1)` in space by overwriting values of `sub` into original `nums` array.

# DP Approach
The idea is to start from the end and for every index i, iterate over all the next elements till the end of array and find the lis
Since lis of a single element is always 1, the recurrence relation is 
`lis[i] = max(1, 1 + lis[j])`

Refer: [Neetcode](https://www.youtube.com/watch?v=cjWnW0hdF1Y)

code:
```cpp
class Solution {
    // returns length of lis starting at i
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

- Time: `O(N ^ 2)`
- Space: `O(N)`