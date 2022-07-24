#twopointers

The problem is similar to 3Sum except we need to return a `List<List<Integer>`.
Approach is to use two pointers, low and high after sorting the array.
Steps:
1. Sort the array
2. Initialize variable i to 1, and j to i + 1.
3. If previous value and current element of i and j are equal, just skip the value
4. Initialise 2 pointers - low and high at j + 1 and array length - 1 resp.
5. Calculate sum of elements at i , j , low and high and current element is equal to target. Note that sum can be greater than int max hence use long 
6. If sum == target, add elements to List and increment low and decrement high.
     Escape the duplicate elements.
7. If sum < target, increment low.
8. if sum > target, decrement high.

``` java
 public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        if(nums == null || nums.length < 4) return result;
        Arrays.sort(nums);
        
        for(int i = 0; i<nums.length - 3; i++)
        {
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            
            for(int j = i + 1; j < nums.length - 2; j++)
            {
                if(j > i + 1 && nums[j] == nums[j - 1]) continue;
                int low = j + 1, high = nums.length - 1;
                while(low < high)
                {
                    long currSum = (long)nums[i] + (long)nums[j] + (long)nums[low] + (long)nums[high];
                    if(currSum == target)
                    {
                        List<Integer> res= new ArrayList<>();
                        res.add(nums[i]);
                        res.add(nums[j]);
                        res.add(nums[low]);
                        res.add(nums[high]);
                        result.add(res);
                         low++;
                        high--;
                        while(low < high && nums[low] == nums[low - 1]) {low++;}
                        while(low < high && nums[high] == nums[high + 1]) {high--;}
                       
                    }
                   else if(currSum < target)
                   {
                       low++;
                   }
                    else
                    {
                    high--;
                    }     
                }
            }
        }
        return result;
    }
```