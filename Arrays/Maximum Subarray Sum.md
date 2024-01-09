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

This implementation does not pass when all the elements in the input array are negative. In such a case, the above implementation returns `0` (empty subarray).

If a non-empty subarray is required and the input array contains all negative elements, the result has to be greatest negative element. So the algorithm can be tweaked to keep track of the max element in the array. This way, when all elements are negative, `mxHere` becomes `0`, max element of array becomes the result.
In case the array contains `0`, that becomes the largest element.

```cpp
int maxSubarraySum(std::vector<int>& nums) {
	int mxHere = 0, mxSoFar = INT_MIN, mxElement = INT_MIN;
	for (auto& x: nums) {
		mxHere += x;
		if (mxHere < 0)
			mxHere = 0;
		mxSoFar = std::max(mxSoFar, mxHere);
		mxElement = std::max(mxElement, x);
	}
	if (mxHere == 0)
		mxSoFar = mxElement;
	return mxSoFar;
}
```