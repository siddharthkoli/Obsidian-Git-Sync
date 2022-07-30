The **lower_bound()** method in C++ is used to return an iterator pointing to the first element in the range \[first, last) which has a value not less than val. 
This means that the function returns an iterator pointing to the next smallest number just greater than or equal to that number. 
If there are multiple values that are equal to val, lower_bound() returns the iterator of the first such value.

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 30 at index 2

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 35 at index 3

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 55 at index 5 (Basically, 55 is not present, so it returns end() iterator)

**Input:** 10 20 30 30 30 40 50  
**Output:** lower_bound for element 30 at index 2