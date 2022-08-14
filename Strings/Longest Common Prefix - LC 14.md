# Horizontal Scanning
![[Pasted image 20220814162119.png]]
![[Pasted image 20220814162130.png]]

```cpp
class Solution {
	string commonPrefix(string& currPrefix, string& s) {
		int minLength = min(currPrefix.length(), s.length());
		for (int i = 0; i < minLength; i++) {
			if (currPrefix[i] != s[i])
				return currPrefix.substr(0, i);
		}
		return currPrefix.substr(0, minLength);
	}

public:
	string longestCommonPrefix(vector<string>& strs) {
		string prefix = strs[0];
		for (int i = 1; i < strs.size(); i++) {
			prefix = commonPrefix(prefix, strs[i]);
			if (prefix == "")
				break;
		}
		return prefix;
	}
};
```
- Time: `O(S)` where `S` is the sum total of all characters in `strs`.
- Space: `O(1)`