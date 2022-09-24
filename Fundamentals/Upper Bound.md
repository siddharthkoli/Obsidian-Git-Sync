 It returns an iterator pointing to the first element in the range \[first, last) that is greater than value, or last if no such element is found.

***Subtracting the first position i.e vect.begin() from the pointer, returns the actual index.***

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