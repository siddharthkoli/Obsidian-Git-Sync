Let's assume we have a fixed size of window (`minSize`), we can easily use a sliding window of that size and check for the contraints within that window.  
This can be done in `O(n)` using a hashmap to store the unique count of letters in the window.

The greedy part of the solution is that, we also notice that we only need `minSize` since if the `minSize` satisfies the constraints to have `distinct letters <= maxLetters` any substring greater than that size would only add at max a new distinct letter.  
Which esentially means that since the substring of size greater than minSize starisfies the constraint of `distinct letters <= maxLetters` there will be a substring of this selected substring of size minSize that'll satisfy the same constraint and the frequency of this substring will be atleast as much as the parent substring.  
We also know that number of shorter substrings are more than the longer ones , thus we only need to check for substrings of minSize satisfying the condition.

Eg: `s=abcabc, minSize=3, maxSize=6, maxLetter=3`  
substrings satisfying the constraints are `abc`, `abca` ,`abcab`, `abcabc`, `bca`, `bcab`, `bcabc`, `cab`, `cabc` and `abc` again, we can see that all the substrings have a substring within it of `size=minSize` that satisfies all the conditions, like we have `abc` in first 4 substrings. Thus we only need to check for substrings of `size=minSize` that satisfy the condition to get our result.

```cpp
class Solution {
public:
    // Time: O(N) Space: O(N)
    int maxFreq(string s, int maxLetters, int minSize, int maxSize) {
        int n = s.length(), start = 0, end = 0, mx = 0;
        
        std::unordered_map<char, int> hash;
        std::unordered_map<string, int> substrFreq;

        while (end < minSize - 1)
            hash[s[end++]]++;

        while (end < n) {
            hash[s[end]]++;
            string curr = s.substr(start, minSize);
            substrFreq[curr]++;
            
            if (hash.size() <= maxLetters)
                mx = std::max(mx, substrFreq[curr]);
            
            hash[s[start]]--;
            if (hash[s[start]] == 0)
                hash.erase(s[start]);
            start++, end++;
        }
        
        return mx;
    }
};
```