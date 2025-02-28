Its obvious to replace characters with the character that has the highest frequency.
No. of characters to replace is given by windowSize - freq. of max element in window.

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        int n = s.length();
        int res = 0, start = 0, end = 0;

        unordered_map<char, int> hash;
        int mx = 0;
        
        while (end < n) {
            hash[s[end]]++;
            mx = max(mx, hash[s[end]]);

            while (start < end && end - start + 1 - mx > k) {
                hash[s[start]]--;
                if (hash[s[start]] == 0)
                    hash.erase(s[start]);
                start++;
            }

            res = max(res, end - start + 1);
            end++;
        }

        return res;
    }
};

```