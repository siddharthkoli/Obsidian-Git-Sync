#heaps
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
- Time: `O(N * logK)`.
- Space: `O(N)`

# Approach 2: Using buckets
1. Observe the fact that the max frequency for any element can be the size of the array.
2. So create a `bucket` array of size `n` where `bucket[i]` holds all the elements whose frequency is `i`.
3. Start iterating from the back of `bucket` since we need to find elements with highest frequency
4. Keep adding elements to `result` vector untill size of `result` becomes `k`.

```cpp
class Solution {
    
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        std::vector<int> result;
        // time: O(N), space: O(N)
        std::unordered_map<int, int> hash;
        // O(N)
        // calculate frequency of elements
        for (auto x: nums)
            hash[x]++;
        
        // create a bucket of frequency -> vector of elements with said freq
        // the max freq elem. can have is the size of nums
        std::vector<std::vector<int>> bucket(nums.size() + 1);
        // O(N)
        for (auto x: hash)
            bucket[x.second].push_back(x.first);
        
        bool done = false;
        // O(N) start from back and take k elements
        // in the worst case where all elements appear once, index 1 will have all the elements in the bucket
        // so time comp = 
        // O(N) -> moving from back to first bucket + O(N) -> iterating over all elements in the bucket
        // total: O(N)
        for (int i = nums.size(); i > 0; i--) {
            for (auto x: bucket[i]) {
                result.push_back(x);
                if (result.size() == k) {
                    done = true;
                    break;
                }
            }
            if (done)
                break;
        }
        return result;
    }
};
```
- Time: `O(N)` when elements can be returned in any order. `O(N + K * logK)` when elements have to be returned in sorted order.
- Space: `O(N)`