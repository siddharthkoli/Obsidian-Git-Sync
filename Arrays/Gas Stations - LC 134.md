#greedy 
First of all, calculate the sum of `gas` and sum of `cost`. 
If sum of `gas` < sum of `cost`, it is impossible to perform a loop since you simply do not have enough gas that matches the required cost.

If the above check passes, that means there exists a solution. The constraints guarantee that there will always be a unique solution.
Start moving greedily from the start of the array, while keeping track of the difference between the `gas[i]` and `cost[i]`
	`total += gas[i] - cost[i]`
if `total` < 0, you cannot move ahead and therefore, the chosen start was invalid.
But since passing the initial sum of `gas` and sum of `cost` check guaranteed a solution, you can greedily consider the next index as a potential start.

```cpp
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
	int gasSum = std::accumulate(gas.begin(), gas.end(), 0);
	int costSum = std::accumulate(cost.begin(), cost.end(), 0);
	
	// if cost becomes greater than gas available, no loop is possible
	if (gasSum < costSum)
		return -1;
	
	// since gasSum >= costSum, it is guaranteed that there exists one
	// way to loop through.
	int total = 0, result = 0;
	for (int i = 0; i < gas.size(); i++) {
		total += gas[i] - cost[i];
		if (total < 0) {
			total = 0;
			result = i + 1;
		}
	}
	return result;
}
```
- Time: `O(N)`
- Space: `O(1)`