![[Pasted image 20220730183431.png]]
![[Pasted image 20220730183449.png]]

```cpp
class Solution {
    // refer: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/discuss/75928/Share-my-DP-solution-(By-State-Machine-Thinking)
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        // time: O(N)
        // space: O(1)
        // space optimized version of below version
        #if 1
        int buy, sell, rest;
        buy = -prices[0], sell = 0, rest = 0;
        for (int i = 1; i < n; i++) {
            // there is no way to know previous sell i.e. b[i-1]
            // since sell is directly updated
            // hence store prevSold
            int prevSold = sell;
            buy = std::max(buy, rest - prices[i]);
            sell = buy + prices[i];
            rest = std::max(rest, prevSold);
        }
        return std::max(sell, rest);
        #endif
        
        // time: O(N)
        // space: O(N)
        #if 0
        std::vector<int> a(n), b(n), c(n);
        a[0] = -prices[0], b[0] = 0, c[0] = 0;
        
        for (int i = 1; i < n; i++) {
            a[i] = std::max(a[i-1], c[i-1] - prices[i]);
            b[i] = a[i-1] + prices[i];
            c[i] = std::max(c[i-1], b[i-1]);
        }
        
        return std::max(b[n - 1], c[n - 1]);
        #endif
    }
};
```
