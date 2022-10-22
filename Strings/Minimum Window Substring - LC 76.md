```cpp
class Solution {
public:
    // refer neetcode (https://www.youtube.com/watch?v=jSto0O4AJbM)
    string minWindow(string s, string t) {
        std::unordered_map<char, int> window, total;
        for (auto x: t)
            total[x]++;
        int left = 0, right = 0, have = 0, need = total.size();
        int mn = INT_MAX, minStart = 0;
        while (right < s.length()) {
            window[s[right]]++;
            if (window[s[right]] == total[s[right]])
                have++;
            while (have == need) {
                if (right - left + 1 < mn) {
                    mn = right - left + 1;
                    minStart = left;
                }
                window[s[left]]--;
                if (window[s[left]] < total[s[left]])
                    have--;
                left++;
            }
            right++;
        }
        return mn == INT_MAX ? "" : s.substr(minStart, mn);
    }
};
```
- Time: `O(N + M) [N = s.length(), M = t.length()]`
- Space: `O