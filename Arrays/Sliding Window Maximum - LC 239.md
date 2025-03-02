2 methods:
### Method 1: `O(N * LogN)` time
The idea is to keep a `map` or `multiset` that has all the items that are in the current window. the max element will always be at the end.
Using a `map` is straighforward by reducing the freq count.
If using a `multiset`, `multiset.erase()` will erase all occurrences of that element. So acquire a pointer to that element and then erase that.

### Method 2: Using `deque` for `O(N)` time `O(K)` space
The idea is to use a ***monotonic*** `deque` to keep of the elements in the window. Since it is monotonic, the max element will be at the `front` of the `deque`. 

*Why monotonic?*
Since the `deque` is supposed to only hold elements that are in the window, we will need to know what is the next max element when the current max goes out of the window.

*How do we know when the current max is out of the window?*
Instead of storing the actual elements in the `deque`, we could store the indices of the elements. That way if the `start` pointer goes ahead of `deque.front()`, even if it's the max, it's not present in the window and we can pop it. And since the `deque` is monotonic, the next highest in the window will be at `deque.front()`.

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        int start = 0, end = 0;
        std::deque<int> deque;
        vector<int> res;
        while (end < n) {
            while (!deque.empty() && nums[end] > nums[deque.back()])
                deque.pop_back();

            deque.push_back(end);

            if (deque.front() < start)
                deque.pop_front();

            if (end - start + 1 >= k) {
                res.push_back(nums[deque.front()]);
                start++;
            }

            end++;
        }

        return res;
    }
};
```

Time: `O(N)`
Space: `O(K)`