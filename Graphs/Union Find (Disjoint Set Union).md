```cpp
class DS {
	std::vector<int> parent;
    std::vector<int> size;
    
public:
    DS(int v) : parent(v), size(v, 1) {
        for (int i = 0; i < v; i++)
            parent[i] = i;
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