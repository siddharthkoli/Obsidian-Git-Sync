Total allowed transactions is 2
1.  There should be **at most** two transactions, it means possibilities are 0,1,2
2.  You cannot buy 2 stocks at same time, you have to sell one stock before buying a new.
![[Pasted image 20220910235246.png]]
The reason for 5 states is that there are atmost 2 transactions allowed i.e. it is a fixed number unlike saying atmost k transactions.
So we know exactly how many transactions can occur (0, 1 or 2).
Hence we fix total states.
The state equation for each node:  
**x\[i]=x\[i-1];  
y\[i]=max(x\[i-1]-prices\[i], y\[i-1]);  
z\[i]=max(y\[i-1]+prices\[i],z\[i-1]);  
a\[i]=max(a\[i-1],z\[i-1]-prices\[i]);  
b\[i]=max(a\[i-1]+prices\[i],b\[i-1]);**
```cpp
class Solution {
public:
    // state machine solution
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        // time: O(N)
        // space: O(N)
        #if 0
        std::vector<int> a(n), b(n), c(n), d(n), e(n);
        b[0] = d[0] = -prices[0];
        for (int i = 1; i < n; i++) {
            a[i] = a[i-1];
            b[i] = std::max(b[i-1], a[i-1] - prices[i]);
            c[i] = std::max(c[i-1], b[i-1] + prices[i]);
            d[i] = std::max(d[i-1], c[i-1] - prices[i]);
            e[i] = std::max(e[i-1], d[i-1] + prices[i]);
        }
        return std::max({a.back(), c.back(), e.back()});
        #endif
        
        // space optimized version of above solution
        // time: O(N)
        // space: O(1)
        #if 1
        int a, b, c, d, e;
        a = b = c = d = e = 0;
        b = d = -prices[0];
        for (int i = 1; i < n; i++) {
            b = std::max(b, a - prices[i]);
            c = std::max(c, b + prices[i]);
            d = std::max(d, c - prices[i]);
            e = std::max(e, d + prices[i]);
        }
        return std::max({a, c, e});
        #endif
    }
};
```