#twopointers

The problem is similar to 3Sum except we need to return a List<List<Integer>.
Approach is to use two pointers, low and high after sorting the array.
Steps:
1. Sort the array
2. Initialize variable i to 1, and j to i + 1.
3. If previous value and current element of i and j are equal, just skip the value
4. Initialise 2 pointers - low and high at j + 1 and array length - 1 resp.
5. Calculate sum of elements at i , j , low and high and current element is equal to target. Note that sum can be greater than int max hence use long 
6. If sum == target, add elements to List and increment low and decrement high.
     Escape the