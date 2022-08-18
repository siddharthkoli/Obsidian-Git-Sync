##### <u>The problem has to be solved in linear time and using constant space.</u>
Linear time and constant space constraints suggest modifying the exisiting array to solve the problem.

We are looking for numbers beginning from 1.
Notice that our answer always lies between 1 and N + 1 i.e. \[1, N + 1].
If all nos are less than or equal to 0, answer will be 1.
If array contains nos from 1 to N, then answer will be N+1.
If array contains mixture of nos, then answer 