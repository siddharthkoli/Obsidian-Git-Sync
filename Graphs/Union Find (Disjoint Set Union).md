```cpp
class DS {
	void make_set(int v) { 
		parent[v] = v; 
		rank[v] = 0; 
	}
	
	int find_set(int v) {
	    if (v == parent[v])
	        return v;
	    return parent[v] = find_set(parent[v]);
	}

	void union_sets(int a, int b) {
	    a = find_set(a);
	    b = find_set(b);
	    if (a != b) {
	        if (rank[a] < rank[b])
	            swap(a, b);
	        parent[b] = a;
	        if (rank[a] == rank[b])
	            rank[a]++;
	    }
	}
}
```
- Time: if we combine both optimizations - path compression with union by size / rank - we will reach nearly constant time queries. It turns out, that the final amortized time complexity is `O(α(n))`, where `α(n)` is the inverse Ackermann function, which grows very slowly. In fact it grows so slowly, that it doesn't exceed 4 for all reasonable `n` (approximately `n < 10e600`).