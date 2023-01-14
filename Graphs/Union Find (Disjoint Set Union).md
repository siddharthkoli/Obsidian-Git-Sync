```cpp
class DS {
    std::vector<int> parent;
    std::vector<int> size;
    
public:
    DS(int n) : parent(n), size(n, 1) {
        for (int i = 0; i < n; i++)
            parent[i] = i;
    }

	/* returns a const reference to the private parent container
	   since there is no way to access parent if required from outside.
	*/
    std::vector<int> const& getParent() const {
        return parent;
    }
        
    int _find(int v) {
        if (v == parent[v])
            return v;
        return parent[v] = _find(parent[v]);
    }
    
    void _union(int a, int b) {
        a = _find(a);
        b = _find(b);
        
        if (a != b) {
            if (size[a] < size[b])
                std::swap(a, b);
            parent[b] = a;
            size[a] += size[b];
        }
    }
    
};
```
- Time: if we combine both optimizations - path compression with union by size / rank - we will reach nearly constant time queries. It turns out, that the final amortized time complexity is `O(α(n))`, where `α(n)` is the inverse Ackermann function, which grows very slowly. In fact it grows so slowly, that it doesn't exceed 4 for all reasonable `n` (approximately `n < 10e600`).

<hr/>

***To find number of connected components:***

`parent` array stores the parent or root of every vertex. So the number of distinct parents will give total number of connected components.