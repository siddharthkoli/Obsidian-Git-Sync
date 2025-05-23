The **lower_bound()** method in C++ is used to return an iterator pointing to the first element in the range \[first, last) which has a value not less than val. 
This means that the function returns an iterator pointing to the next smallest number just greater than or equal to that number. 
If there are multiple values that are equal to val, lower_bound() returns the iterator of the first such value.

***Subtracting the first position i.e vect.begin() from the pointer, returns the actual index.***

***In case where the element to find is occurring multiple times,***
- `lower_bound` will give the first occurrence of it.
- `prev(upper_bound)` will give the last occurrence of it.

```cpp
std::vector<int> a = {1, 2, 2, 2, 2, 2, 3, 4, 5};
//                    0, 1, 2, 3, 4, 5, 6, 7, 8  

cout << "lower bound: " << lower_bound(a.begin(), a.end(), 2) - a.begin() << endl;

cout << "upper bound: " << upper_bound(a.begin(), a.end(), 2) - a.begin() << endl;

cout << "prev upper bound: " << prev(std::upper_bound(a.begin(), a.end(), 2)) - a.begin() << endl;

OUTPUT:
lower bound: 1
upper bound: 6
prev upper bound: 5
```

**To summarize returns:**
 -  Returns pointer to the position of num if the container contains only **one occurrence** of num
 - Returns a pointer to the first position of num if the container contains **multiple occurrences** of num.
 - Returns pointer to the position of a number just higher than num, if the container **does not contain an occurrence** of num

```cpp
	vector<int> arr1 = { 10, 15, 20, 25, 30, 35 };

	vector<int> arr2 = { 10, 15, 20, 20, 25, 30, 35 };

	vector<int> arr3 = { 10, 15, 25, 30, 35 };
```
**Output**

```cpp
The position of 20 using lower_bound  (in single occurrence case) : 2
The position of 20 using lower_bound (in multiple occurrence case) : 2
The position of 20 using lower_bound (in no occurrence case) : 2
```

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 30 at index 2

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 35 at index 3

**Input:** 10 20 30 40 50  
**Output:** lower_bound for element 55 at index 5 (Basically, 55 is not present, so it returns end() iterator)

**Input:** 10 20 30 30 30 40 50  
**Output:** lower_bound for element 30 at index 2