#graphs #shortestpath
Gives shortest path from `source` to all nodes in the graph

```cpp
vector<int> shortestPath(vector<vector<pair<int, int>>>& adj, int source) {
	int n = adj.size();
	vector<int> distance(n, INT_MAX);

	priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq; // pq with smallest element at the top

	distance[source] = 0;
	pq.push({0, source});

	while (!pq.empty()) {
		auto [currCost, u] = pq.top();
		pq.pop();

		// ignoring stale entries in the pq that were inserted earlier
		// but since then the distance array was updated for that node
		if (distance[u] < currCost)
			continue;

		for (auto& [v, edgeCost]: adj[u]) {
			int newCost = currCost + edgeCost;
			if (newCost < distance[v]) {
				distance[v] = newCost;
				pq.push({newCost, v});
			}
		}
	}

	return distance;
}
```

#### Time Complexity:
`O(E * log V)` - Relaxing edges: O(E) to iterate over all edges, and O(log V) to update the priority queue for each edge, resulting in O(E log V)

#### Space Complexity:
`O(V + E)` -
- Distance array: O(V) to store the shortest distances from the source node
- Priority queue: O(V) to store the vertices to be processed.
- Adjacency list or matrix: O(E) to store the graph edges