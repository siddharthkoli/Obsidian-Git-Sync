#hashmap #subarray 
This approach can be implemented in 2 ways:
	1. add 0 sum to hash before beginning and then add sum - k to cnt
    2. dont add 0 at beginning but cnt++ anytime sum == k
(dont do both together)
```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int cnt = 0;
        int n = nums.size();
        unordered_map<int, int> hash;
        int prefixSum = 0;
        hash[0] = 1;
        for (int i = 0; i < n; i++) {
            prefixSum += nums[i];
            // if (prefixSum == k)
            //     cnt++;
            if (hash.find(prefixSum - k) != hash.end())
                cnt += hash[prefixSum - k];
            hash[prefixSum]++;
        }
        return cnt;
    }
};
```
- Time: `O(N)`
- Space: `O(N)`