We can perform 3 actions:
 - Buy
 - Sell
 - Wait
This results in 2 states starting from `A`.
![[Pasted image 20220910202943.png]]
Note: The result will be `a[n-1]` and not `b[n-1]`. 
This is because on `b`, we have bought a stock and are possibly holding it. That means we have put in money. Any profit can happen when we move out of this state i.e. transition from `b` to `a`. Hence `a` holds profit.
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        std::vector<int> a(n), b(n);
        b[0] = -prices[0];
        for (int i = 1; i < n; i++) {
            a[i] = std::max(a[i-1], b[i-1] + prices[i]);
            b[i] = std::max(b[i-1], a[i-1] - prices[i]);
        }
        return a[n-1];
    }
};
```

- Time: `O(N)`.
- Space: `O(N)`