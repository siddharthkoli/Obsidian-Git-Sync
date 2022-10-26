#hashmap #subarray 
```cpp
class Solution {
public:
    bool checkSubarraySum(vector<int>& nums, int k) {
        std::unordered_map<int, int> hash;
        hash[0] = 0;
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            // important point to remember is not to update the hash of any
            // element if it exists.
            // We have to maintain the first occurence of the hash
            if (hash.find(sum % k) == hash.end())
                hash[sum % k] = i + 1;
            else if (hash[sum % k] < i) // subarray with size > 1 exists
                return true;
        }
        return false;
    }
};
```
- Time: `O(N)`
- Space: `O(N)`