 It returns an iterator pointing to the first element in the range \[first, last) that is greater than value, or last if no such element is found.

*To find number that is atmost X, find previous of upper_bound of X. refer: [[AtCoder - Exponential]]*

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

**Summarize return values:**
 - Returns pointer to the position of next higher number than num if the container contains **one occurrence** of num.
 - Returns pointer to the first position of the next higher number than the last occurrence of num if the container contains **multiple occurrences** of num.
 - Returns pointer to position of next higher number than num if the container **does not contain an occurrence** of num.

```cpp
	vector<int> arr1 = { 10, 15, 20, 25, 30, 35 };

	vector<int> arr2 = { 10, 15, 20, 20, 25, 30, 35 };

	vector<int> arr3 = { 10, 15, 25, 30, 35 };
```
**Output**

```cpp
The position of 20 using upper_bound (in single occurrence case) : 3
The position of 20 using upper_bound (in multiple occurrence case) : 4
The position of 20 using upper_bound (in no occurrence case) : 2
```


**Input** : 10 20 30 30 40 50
**Output** : upper_bound for element 30 is at index 4

**Input** : 10 20 30 40 50
**Output** : upper_bound for element 45 is at index 4

**Input** : 10 20 30 40 50
**Output** : upper_bound for element 60 is at index 5