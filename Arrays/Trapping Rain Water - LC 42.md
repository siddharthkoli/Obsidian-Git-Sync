2 ways to solve

at any given column, the amount of water it stores can be calculated by:
`watter at i = min(maxLeft, maxRight) - heights[i]`
because the highest level of water is determined by the min of both leftMax and rightMax. And the blocks at the bottom of index i are just subtracted from those.
### Method 1: Uses extra space

Essentially, all we need to know is for any index i is the maxLeft and maxRight columns that are closest to it. We can do it in 2 passs