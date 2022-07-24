#twopointers

The problem is similar to 3Sum except we need to return a List<List<Integer>.
Approach is to use two pointers, low and high after sorting the array.
Steps:
1. Sort the array
2. Initialize variable i to 1, and j to i + 1.
3. If previous value and current element of i and j are equal, just skip the value
4. Calculate sum of elements at i , j , low and high and current elemen