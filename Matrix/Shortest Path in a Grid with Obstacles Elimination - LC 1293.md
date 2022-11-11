#BFS
`if(vis[x][y]!=-1 && vis[x][y]>=t[3])` has 2 conditions. Both the conditions are explained below
1.  `vis[x][y]!=-1` checks if the cell has already been visited.
2.  `vis[x][y]>=t[3]` checks if we have already reached the cell via some previous path by removing ***lesser**** obstacles in that previous path. If we have reached the current cell via some previous path by removing ***lesser*** obstacles, it means that we have a greater chance of using this previous path to reach the destination, because we have scope to remove ***more*** obstacles in the upcoming un-visited cells using the previous path than using the current path.

```cpp
class Solution {
public:
    int shortestPath(vector<vector<int>>& grid, int k) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<int>> visited(m, vector<int>(n, -1)); // value > -1 indicates how many more obstacles we can still remove while also indicating if cell is visited
        
        std::queue<vector<int>> queue; // x, y, curr path length, no. of obstacles that we can still remove
        queue.push({0, 0, 0, k});
        
        int dx[] = {-1, 1, 0, 0};
        int dy[] = {0, 0, -1, 1};
        
        while (!queue.empty()) {
            auto curr = queue.front();
            queue.pop();
            int x = curr[0], y = curr[1];
            if (x < 0 || y < 0 || x >= m || y >= n)
                continue;
            
            if (x == m - 1 && y == n - 1)
                return curr[2];
            
            if (grid[x][y] == 1) {
                if (curr[3] <= 0) // if we encounter an obstacle, we can remove it
                    continue;
                curr[3]--;
            }
            
            if (visited[x][y] != -1 && visited[x][y] >= curr[3])
                continue;
            visited[x][y] = curr[3];
            
            for (int i = 0; i < 4; i++)
                queue.push({x + dx[i], y + dy[i], curr[2] + 1, curr[3]});
        }
        
        return -1;
    }
};
```
- Time: `O(M * N * K)`
- Space: `O(M * N * K)`