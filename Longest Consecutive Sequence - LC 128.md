The idea is to find the start of every sequence. A number where number-1 doesnt exist in the array is the start of the sequence.

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        std::unordered_set<int> hash;
        for (auto x: nums)
            hash.insert(x);
        int mx = 0;
        for (auto num: nums) {
            // if num - 1 is present in hash
            // that means num is part of a sequence that may already have been processed
            // so skip it
            if (hash.find(num - 1) != hash.end())
                continue;
            int curr = num;
            while (hash.find(curr) != hash.end())
                curr++;
            mx = std::max(mx, curr - num);
        }
        return mx;
    }
};
```

Time: `O`