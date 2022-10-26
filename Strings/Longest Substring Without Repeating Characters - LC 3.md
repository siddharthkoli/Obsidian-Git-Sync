```cpp
int lengthOfLongestSubstring(string s) {
        std::unordered_map<char, int> hash;
        int start = 0, end = 0;
        int mx = 0;
        while (end < s.length()) {
            hash[s[end]]++;
            while (hash[s[end]] > 1) {
                hash[s[start]]--;
                start++;
            }
            mx = std::max(mx, end - start + 1);
            end++;
        }
        return mx;
}
```
- Time: `O(N)`
- Space: `O(N)`