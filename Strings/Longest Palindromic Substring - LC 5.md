```cpp
class Solution {
    bool palindrome(int start, int end, string s) {
        int n = s.length();
        int i = start, j = end - 1;
        while (i < j) {
            if (s[i++] != s[j--])
                return false;
        }
        return true;
    }
    
    bool palindrome(string s, int start, int end, vector<vector<bool>>& dp) {
        if (start == end)
            return dp[start][end] = true;
        
        if (start == end - 1)
            return dp[start][end] = s[start] == s[end];
        
       return dp[start][end] = s[start] == s[end] && palindrome(s, start + 1, end - 1, dp);
    }
    
    int expandAroundCenter(string s, int start, int end) {
        while (start < s.length() && end >= 0 && s[start] == s[end])
            start--, end++;
        return end - start - 1; // subtract 1 since chars at start and end are not same
    }

public:
    string longestPalindrome(string s) {
        // expanding from center
        // time: O(N ^ 2) Space: O(1)
        // there are 2n - 1 valid centers
        #if 1
        int n = s.length(), mx = 1, startIndex = 0;
        for (int i = 0; i < n; i++) {
            int len1 = expandAroundCenter(s, i, i);
            int len2 = expandAroundCenter(s, i, i + 1);
            int mxLen = std::max(len1, len2);
            if (mxLen > mx) {
                mx = mxLen;
                startIndex = i - (mxLen - 1) / 2;
            }
        }
        return s.substr(startIndex, mx);
        #endif
        
        #if 0
        // bottom up dp
        // Time: O(N ^ 2) Space: O(N ^ 2)
        int n = s.length(), mx = 1, startIndex;
        
        // dp[i][j] will be false if
        // substring s[i...j] is not palindrome
        vector<vector<bool>> dp(n, vector<bool>(n));

        // all substrs of len 1 are palindrome
        for (int i = 0; i < n; i++)
            dp[i][i] = true;
        
        // all substrs with length 2 will be palindromes
        // if both the chars are same
        for (int i = 0; i < n - 1; i++) {
            if (s[i] == s[i+1]) {
                dp[i][i+1] = true;
                mx = 2;
                startIndex = i;
            }
        }
        
        // fix length of curr substr
        // check for lengths > 2
        for (int len = 3; len <= n; len++) {
            // fix start, calc end.
            // compute dp table for all substrs of length len
            // between s[start...end]
            for (int start = 0; start + len - 1 < n; start++) {
                int end = start + len - 1;
                dp[start][end] = s[start] == s[end] && dp[start+1][end-1];
                if (dp[start][end]) {
                    mx = end - start + 1;
                    startIndex = start;
                }
            }
        }
        
        return s.substr(startIndex, mx);
        #endif
        
        #if 0
        // top down dp
        // Time: O(N ^ 2) Space: O(N ^ 2)
        int n = s.length(), mx = 0, startIndex = 0;
        vector<vector<bool>> dp(n, vector<bool>(n));

        for (int len = 1; len <= s.length(); len++) {
            for (int start = 0; start + len - 1 < n; start++) {
                int end = start + len - 1;
                if (palindrome(s, start, end, dp) && len > mx) {
                    mx = len;
                    startIndex = start;
                }
            }
        }
        
        return s.substr(startIndex, mx);
        #endif
        
        #if 0
        // brute force
        // iterate over all possible substrings
        // 1 optimization is that we check for longest strings first since we want the longest palindrome
        // time: O(N ^ 3). Space: O(1)
        int n = s.length(), mx = 1;
        string res = "";
        
        for (int len = s.length(); len > 0; len--) {
            for (int start = 0; start + len <= s.length(); start++) {
                if (palindrome(start, start + len, s))
                    return s.substr(start, len);
            }
        }
        
        return "";
        #endif
    }
};
```