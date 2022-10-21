# Approach 1: Minheap
***Refer to [[C++ Comparator]] for writing comparators for priority queue***
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
- Time: `O(N * log K * M)` `M` is size of each string.
- Space: `O(K)`

# Approach 2: Quickselect
- STL Version
```cpp
class Solution {
public:
    string kthLargestNumber(vector<string>& nums, int k) {
        std::nth_element(nums.begin(), nums.begin() + k, nums.end(), [&](const string a, const string b) {
            if (a.length() == b.length())
                return a < b;
            return a.length() < b.length();
        });
        return nums[k];
    }
};
```
- Time: `O(N * M)` where `M` is size of each string.
- Space: `O(1)`
***Writing custom implementation of quickselect is tough to fit in linear time.***
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
    // cannot compare by converting strings to int using std::stoi
    // because nums[i].length <= 100.
    // hence compare by lengths and worst case digit by digit.
    bool xLessThanEqualToY(const string& a, const string& b) {
        if (a.length() == b.length())
            return a < b;
        return a.length() < b.length();
    }
    
    int quickselect(std::vector<string>& nums, int left, int right, int k) {
        string pivot = nums[right];
        int currInd = left;
        for (int i = left; i < right; i++) {
            if (xLessThanEqualToY(nums[i], pivot)) {
                std::swap(nums[i], nums[currInd]);
                currInd++;
            }
        }
        std::swap(nums[currInd], nums[right]);
        if (currInd == k)
            return currInd;
        if (currInd < k)
            return quickselect(nums, currInd + 1, right, k);
        return quickselect(nums, left, currInd - 1, k);
    }
    
public:
    string kthLargestNumber(vector<string>& nums, int k) {
        // quickselect
        // time: O(N * length of string), space: O(1) excluding recursion
        int n = nums.size();
        k = n - k; // kth largest is n - k from start
        
        #if 0
        // custom quickselect implementation.
        // TLE
        return nums[quickselect(nums, 0, n - 1, k)];
        #endif
// ----------------------------------------------------------------------------------------        
        // stl quickselect
        // ACCEPTED
        #if 0
        std::nth_element(nums.begin(), nums.begin() + k, nums.end(), [&](const string a, const string b) {
            if (a.length() == b.length())
                return a < b;
            return a.length() < b.length();
        });
        return nums[k];
        #endif
    }
};
```