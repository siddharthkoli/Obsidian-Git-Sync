Ok, so I read the description again, then I realize, it is asking about some sort of "increasing subsequence" with size 3.

Then I think about all the relevant algorithm I know, for example, the famous "Longest Increasing Subsequence" (LIS) problem.

Then I instantly got a solution: Find the LIS of the input, and if it is greater than 3, return true;  
Looks like a working solution, what's its complexity then:

There is a O(nlogk) solution to LIS (if you don't know it, just search this problem in Leetcode and see the discussions), where n is the array length and k is the length of LIS. Here, k is no larger than 2, so it is O(nlog2) = O(n). Very well, a O(n) solution is so easily obtained here:

```cpp
class Solution {
public:
    // find Longest Increasing Subsequence
    // return when LIS of length 3 is found
    bool increasingTriplet(vector<int>& nums) {
        // greedy with binary search
        #if 0
        std::vector<int> sub;
        sub.push_back(nums[0]);
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > sub[sub.size() - 1])
                sub.push_back(nums[i]);
            else {
                auto itr = std::lower_bound(sub.begin(), sub.end(), nums[i]);
                *itr = nums[i]; // replace with nums[i]
            }
            if (sub.size() >= 3)
                return true;
        }
        return false;
        #endif
        // dp
        // Time: O(N ^ 2)
        // Space: O(N)
        #if 0
        std::vector<int> dp(nums.size(), 1);
        for (int i = nums.size() - 1; i >= 0; i--) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[j] > nums[i])
                    dp[i] = std::max(dp[i], 1 + dp[j]);
                if (dp[i] >= 3)
                    return true;
            }
        }
        return false;
        #endif
    }
};
```

Apparently, as you may have already noticed, the "dp" here contains at most 2 elements, so one instant simplification here is to replace "lower_bound" call to a simple "if comparison else comparison". Then a much more simplified version is obtained:

``` cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int a = INT_MAX, b = INT_MAX;
        for (auto n : nums)
            if (n <= a)
                a = n;
            else if (n <= b)
                b = n;
            else
                return true;
        return false;
    }
};
```

You may have seen 100 ways to explain why this "if .. else" works in other discussions. Here, it is so easy to understand: it is just a simple version of Binary Search for 2 elements -- the replacement of lower_bound in above solution.