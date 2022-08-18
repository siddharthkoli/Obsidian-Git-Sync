##### <u>The problem has to be solved in linear time and using constant space.</u>
Linear time and constant space constraints suggest modifying the exisiting array to solve the problem.

We are looking for numbers beginning from 1.
Notice that our answer always lies between 1 and N + 1 i.e. \[1, N + 1].
If all nos are less than or equal to 0, answer will be 1.
If array contains nos from 1 to N, then answer will be N+1.
If array contains mixture of nos, then answer is first missing no in the range \[1, N]

If using extra space was an option, creating buckets would have been an easy solution.

Creating an array of size N initialized to 0, for every value A\[i] which lies in the range \[1, N], we would have incremented its count in the array. Consequently, we would traverse the array to find the first array position with value 0, hence finding our answer.

However, since we are not allowed buckets, we can use the existing array as bucket somehow.

