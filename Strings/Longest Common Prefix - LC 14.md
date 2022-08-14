# Horizontal Scanning
![[Pasted image 20220814162119.png]]
![[Pasted image 20220814162130.png]]

```cpp
class Solution {
	string commonPrefix(string& currPrefix, string& s) {
		int minLength = min(currPrefix.length(), s.length());
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