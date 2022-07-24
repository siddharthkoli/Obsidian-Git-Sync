#dp, #strings
``` cpp
// returns lcs ending at str1[0..i] and str2[0 ... j]
int lcs(string& str1, string& str2, int i, int j) {
	if (i < 0 || j < 0)
		return 0;
	int mx = 0;
	if (str1[i] == str2[j])
		mx = 1 + lcs(str1, str2, i - 1, j - 1);
	return mx;
}

int lcs(string &str1, string &str2){
	int n = str1.length(), m = str2.length();
	#if 0
	int mx = 0;
	for (int i = n - 1; i >= 0; i--) {
		for (int j = m - 1; j >= 0; j--) {
			mx = std::max(mx, lcs(str1, str2, i, j));
		}
	}
	return mx;
	#endif
	
	// bottom up dp
	#if 1
	std::vector<std::vector<int>> dp(n + 1, std::vector<int>(m + 1));
	for (int j = 0; j <= m; j++)
		dp[0][j] = 0; // "" is common
	for (int i = 0; i <= n; i++)
		dp[i][0] = 0; // "" is common
	
	for (int i = 1; i <= n; i++)
		for (int j = 1; j <= m; j++)
			if (str1[i-1] == str2[j-1])
				dp[i][j] = 1 + dp[i-1][j-1];
	
	// find max element (max value of lcs) from table
	int result = 0;
	for (int i = 1; i <= n; i++)
		result = std::max(result, *std::max_element(dp[i].begin(), dp[i].end()));

	return result;
	#endif
}
```

If the common substring is required as the answer, an `endIndex` variable could be stored which stores the end index of the lcs while finding the max value from the dp table using `*std::max_element()` 

Replace with the following code to get the substring:
``` cpp
int mx = 0;
int endIndex = 0;
for (int i = 1; i <= n; i++) {
	int curr =  *std::max_element(dp[i].begin(), dp[i].end());
		if (curr > mx) {
			mx = curr;
			endIndex = i;
	}
}
		
std::string result = x.substr(endIndex - mx, mx);
return result;
```

time complexity: O(N * M)
space complexity: O(N * M)

The space complexity of the above solution can be improved to O(n) as calculating LCS of a row of the LCS table requires only the solutions to the current row and the previous row.