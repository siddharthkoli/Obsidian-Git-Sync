# Approach 1: Minheap
***Refer to [[C++ Comparator]] for writing comparators for priority queue
```cpp
class MinHeapComp {
public:
    bool operator() (string const& a, string const& b) {
        if (a.length() == b.length())
            return a > b;
        return a.length() > b.length();
    }    
};

class Solution {
public:
    string kthLargestNumber(vector<string>& nums, int k) {
        std::priority_queue<string, std::vector<string>, MinHeapComp> pq;
        for (auto x: nums) {
            pq.push(x);
            if (pq.size() > k)
                pq.pop();
        }
        
        return pq.top();
};
```
- Time: `O(N * log K * M)` M is size of each string.
- Space: `O(K)`

# Approach 2: Quickselect
