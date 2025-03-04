Similar idea to that of [[Sliding Window Maximum - LC 239]]. Maintain a ***monotonic*** `deque`. 
The only difference is in the previous problem, we were looking for the entire max in the window.
Here, we're only looking for the next maximum.
So when were maintaining the monotonic property of the `deque`, i.e. removing smaller elements when a bigger element is at hand, that means we currently have an element that is the bigger than that at hand.
And why is the next bigger? - Because were going at the elements one by one. So it has to be the next max for the one at hand.

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temps) {
        int n = temps.size();
        std::deque<int> deque;
        vector<int> result(n);
        int end = 0;
        while (end < n) {
            while (!deque.empty() && temps[deque.back()] < temps[end]) {
                int ind = deque.back(); deque.pop_back();
                result[ind] = end - ind;
            }

            deque.push_back(end);
            end++;
        }

        while (!deque.empty()) {
            int ind = deque.back(); deque.pop_back();
            result[ind] = 0;
        }

        return result;
    }
};
```

Time: `O(N)`
Space: :`O(N)`