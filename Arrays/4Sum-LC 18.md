#twopointers

The problem is similar to 3Sum except we need to return a List<List<Integer>.
Approach is to use two pointers, low and high after sorting the array.
Steps:
1. Sort the array
2. Initialize variable i to 1, and j to i + 1.
3. To escape duplicates, check if i > 0 and check if previous value of 