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