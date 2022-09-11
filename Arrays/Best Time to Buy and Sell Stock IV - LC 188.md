Extension of [[Best Time to Buy and Sell Stock III - LC 123]]
![[Pasted image 20220911162459.png]]
So for k transactions, number of states required is 2k+1.
While traversing through the states:
 - If k is even we have to take decision to buy or to do nothing  
 - If k is odd we have to take decision to sell or to do nothing.
Note that any of the even states can be the result.
```cpp
class Solution {
public:
    // state machine solution
    // time: O(N * K)
    // space: O(K)
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        if (n == 0 || k == 0)
            return 0;
        int totalStates = 2 * k + 1;
        std::vector<int> state(totalStates);
        
        for (int i = 1; i < totalStates; i += 2)
            state[i] = -prices[0];
        
        for (int i = 1; i < n; i++) {
            // j = 0 will always be 0 since it's the first state
            // so start j from 1
            for (int j = 1; j < totalStates; j++) {
                if (j % 2 == 0) {
                    // sell or wait
                    state[j] = std::max(state[j], state[j-1] + prices[i]);
                } else {
                    // buy or wait
                    state[j] = std::max(state[j], state[j-1] - prices[i]);
                }
            }
        }
        
        int res = 0;
        // all states where we sell can be the result
        // since we can do atmost k transactions
        for (int i = 0; i < totalStates; i += 2)
            res = std::max(res, state[i]);
        
        return res;
    }
};
```
