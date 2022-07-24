#matrix #binarysearch 

Approach 1:
Iterate over all rows. Binary search over all cols
```cpp
int m = matrix.size(), n = matrix[0].size();
for (int i = 0; i < m; i++) {
	if (target >= matrix[i][0] && target <= matrix[i][n-1]) {
		int low = 0, high = n - 1;
		while (low <= high) {
			int mid = low + (high - low) / 2;
			if (matrix[i][mid] == target)
				return true;
			if (matrix[i][mid] < target)
				low = mid + 1;
			else
				high = mid - 1;
		}
	}
}
```

Time: O(M + log N) [ M = row, N = cols ]
Space: O(1)

Approach 2:
Start from the bottom left corner.
Move up if current element is greater 
