#greedy
The general implementation requires that the input array should contain atleast one positive element:
```cpp
int maxSubarraySum(std::vector<int>& nums) {
	int mxHere = 0, mxSoFar = INT_MIN;
	for (auto& x: nums) {
		mxHere += x;
		if (mxHere < 0)
			mxHere = 0;
		mxSoFar = std::max(mxSoFar, mxHere);
	}
	return mxSoFar;
}
```

This implementation does not pass when all the elements in the input array are negative. In such a case, the above implementation gives 