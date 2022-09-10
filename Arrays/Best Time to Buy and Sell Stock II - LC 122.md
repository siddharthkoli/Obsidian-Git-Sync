
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