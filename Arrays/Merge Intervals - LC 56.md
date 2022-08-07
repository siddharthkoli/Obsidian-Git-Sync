1. Sort the array based on `start` value of interval.
2. Sorting guarantees that mergeable intervals will be consecutive
3. If `start` of next interval <= `end` of current interval, it can be merged

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        // time: O(N)
        // space: O(1) not counting output array
        std::sort(intervals.begin(), intervals.end());
        std::vector<std::vector<int>> result;
        result.push_back(intervals[0]);
        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i][0] <= result.back()[1]) {
                result.back()[1] = std::max(result.back()[1], intervals[i][1]);
            } else
                result.push_back(intervals[i]);
        }
        return result;
    }
};
```
- Time: `O(N)`
- Space: `O(1)` not counting output array