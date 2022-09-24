 It returns an iterator pointing to the first element in the range \[first, last) that is greater than value, or last if no such element is found.

**Summarize return values:**
 - Returns pointer to the position of next higher number than num if the container contains **one occurrence** of num.
 - 

**Input** : 10 20 30 30 40 50
**Output** : upper_bound for element 30 is at index 4

**Input** : 10 20 30 40 50
**Output** : upper_bound for element 45 is at index 4

**Input** : 10 20 30 40 50
**Output** : upper_bound for element 60 is at index 5