***Use [[KMP (Knuth Morris Pratt) - String Matching]]***
```cpp
class Solution {
    vector<int> computeLPS(const string& pat) {
        int n = pat.length();
        vector<int> pi(n);
        for (int i = 1; i < n; i++) {
            int j = pi[i-1];
            while (j > 0 && pat[j] != pat[i])
                j = pi[j-1];
            if (pat[j] == pat[i])
                j++;
            pi[i] = j;
        }
        return pi;
    }
public:
    // use kmp
    // time: O(N) - N is length of pattern
    // space: O(N)
    string longestPrefix(string s) {
        vector<int> pi = computeLPS(s);
        int mxLength = pi[s.length() - 1];
        return s.substr(0, mxLength);
    }
};
```
