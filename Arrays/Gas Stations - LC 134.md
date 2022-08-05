#greedy 
First of all, calculate the sum of `gas` and sum of `cost`. 
If sum of `gas` < sum of `cost`, it is impossible to perform a loop since you simply do not have enough gas that matches the required cost.

If the above check passes, that means there exists a solution. The constraints guarantee that there will always be a unique solution.
