# Approach 1: Priority Queue
1. Calculate frequencies using hash map
2. Use min heap with comparator to order elements in priority queue according to their frequencies
3. Maintain the size of queue as `k` by popping when it exceeds `k`.
```cpp
class Solution {
    
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        // (priority queue method) Time complexity: O(N * logK), space: O(N)
        std::unordered_map<int, int> hash;
        // O(N)
        for (auto x: nums)
            hash[x]++;
        
        // comp function will always be called when insertion or deletion of
        // element in queue.
        // cannot use std::less<int> because it will fail for negative numbers
        // eg [4,1,-1,2,-1,2,3], k = 2
        auto comp = [&hash](int x, int y) {
          return hash[x] > hash[y];  
        };
        
        // smallest freq element at the top of queue
        // cannot use max priority_queue since it will remove the most frequent
        // element while popping the queue when queue size is maintained to be k
        std::priority_queue<int, std::vector<int>, decltype(comp)> queue(comp);
        
        // O(NlogK) since heap size is always maintained to be k
        for (auto x: hash) {
            // std::cout << "Inserting -> " << x.first << " Freq -> " << x.second << std::endl;
            queue.push(x.first);
            if (queue.size() > k) {
                // std::cout << "popped -> " << queue.top() << std::endl;
                queue.pop();
            }
        }
                
        while (k--) {
            int curr = queue.top();
            queue.pop();
            result.push_back(curr);
        }
        
        return result;
    }
};
```
- Time: `O(N * logK`.
- Space: `O(N)`

# Approach 2: Using buckets
1. Observe the fact that the max frequency for any element can be the size of the array.
2. So c