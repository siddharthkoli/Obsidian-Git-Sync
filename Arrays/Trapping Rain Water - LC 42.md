2 ways to solve

at any given column, the amount of water it stores can be calculated by:
`watter at i = min(maxLeft, maxRight) - heights[i]`
because the highest level of water is determined by the min of both leftMax and rightMax. And the blocks at the bottom of index i are just subtracted from those.
### Method 1: Uses extra space

Essentially, all we need to know is for any index i is the maxLeft and maxRight columns that are closest to it. We can do it in 2 passes - once left to right for leftMax and then right to left for rightMax.

```cpp
class Solution {
public:
    int trap(vector<int>& heights) {
        int n = heights.size();
        vector<int> left(n), right(n);
        int mx = INT_MIN;
        for (int i = 0; i < n; i++) {
            mx = max(mx, heights[i]);
            left[i] = mx;
        }

        mx = INT_MIN;
        for (int i = n - 1; i >= 0; i--) {
            mx = max(mx, heights[i]);
            right[i] = mx;
        }

        int res = 0;
        for (int i = 0; i < n; i++) {
            int curr = min(left[i], right[i]) - heights[i];
            res += max(0, curr);
        }

        return res;
    }
};
```
Time: `O(N)`
Space: `O(N)`

### Method 2: Uses constant space

Instead of using a vector to store all the left and right max columns, we can use 2 pointers to update them dynamically.
the idea is that if a column is a max column, it'll not hold any water above it. If it's not a max column, there will be water above it. 

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        // time: O(N), space: O(1)
        // refer: https://leetcode.com/problems/trapping-rain-water/discuss/153992/Java-O(n)-time-and-O(1)-space-(with-explanations).
        int n = height.size(), res = 0;
        int left = 0, right = n - 1;
        int maxLeft = 0, maxRight = 0;
        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] > maxLeft)
                    maxLeft = height[left];
                else
                    res += maxLeft - height[left];
                left++;
            } else {
                if (height[right] > maxRight)
                    maxRight = height[right];
                else
                    res += maxRight - height[right];
                right--;
            }
        }
        return res;
    }
};
```
time: `O(N)`
space: `O(1)`