## Steps By Night (`GFG`)
we can't use DP because a loop can get created because the knight may come back to the same position again and again in an infinite loop. Even if we use a visited array to solve this problem its complexity would be n factorial.

Here we have to consider each block in the `2D` matrix as a node denoted by i, j and do `BFS` on the matrix. Here interviewer wants us to figure out that this is a graph problem even though we are not given graph nodes.

```cpp
class Solution 
{
    public:
    bool isValid(int i,int j,int n,vector<vector<bool>>&visited){
       return i >= 0 && i < n && j >= 0 && j < n && !visited[i][j];
    }
	int minStepToReachTarget(vector<int>&KnightPos,vector<int>&TargetPos,int N)
	{
	    int srcx=KnightPos[0]-1,srcy=KnightPos[1]-1,desx=TargetPos[0]-1,desy=TargetPos[1]-1;
	    int posix[8]={2,2,-2,-2,1,-1,1,-1};
	    int posiy[8]={1,-1,1,-1,2,2,-2,-2};
	    queue<pair<int,int>>q;
	    vector<vector<bool>>visited(N,vector<bool>(N,0));
	    q.push({srcx,srcy});
	    visited[srcx][srcy]=1;
	    int count=0;
	    while(!q.empty()){count++;int n=q.size();
	    while(n--){
	        pair<int,int>d=q.front();
	        q.pop();
	        for(int j=0;j<8;j++){
	            int x=d.first+posix[j];
	            int y=d.second+posiy[j];
	            if(desx==x&&desy==y)return count;
	            if(isValid(x,y,N,visited)){visited[x][y]=1;q.push({x,y});}
	        }
	        
	    }
	}return 0;}
}
```

## Rotting Oranges
Push all rotten oranges into the queue and start `BFS`. It is a multi-source `BFS` graph problem.

```cpp
class Solution {
public:
    bool isvalid(int i, int j, vector<vector<bool>>& visited, vector<vector<int>>& grid) {
        return i >= 0 && j >= 0 && j < grid[0].size() && i < grid.size() && !visited[i][j] && grid[i][j] != 0;
    }

    int orangesRotting(vector<vector<int>>& grid) {
        queue<pair<int, int>> q;
        vector<vector<bool>> visited(grid.size(), vector<bool>(grid[0].size(), false));
        
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 2) {
                    q.push({i, j});
                    visited[i][j] = true;
                }
            }
        }
        
        int dirx[4] = {-1, 1, 0, 0};
        int diry[4] = {0, 0, 1, -1};

        int count = 0;
        while (!q.empty()) {
            int n = q.size();
            count++;
            while (n--) {
                auto front = q.front();
                q.pop();
                for (int i = 0; i < 4; i++) {
                    int x = front.first + dirx[i];
                    int y = front.second + diry[i];
                    if (isvalid(x, y, visited, grid)) {
                        grid[x][y] = 2;
                        q.push({x, y});
                        visited[x][y] = true;
                    }
                }
            }
        }
        
        for (int i = 0; i < grid.size(); i++) {
            for (int j = 0; j < grid[0].size(); j++) {
                if (grid[i][j] == 1) return -1;
            }
        }
        
        return count == 0 ? 0 : count - 1;
    }
};
```

## `Topo` Sort
When nodes are dependent on each other or have directed edges and it has to be directed a-cyclic graph.

It tells the order of requirements.

In-degree: of a node is the no. of directed edges towards it.

So a node having 0 in degree is always first in `topo` sort.

`topo` sort not only applies in graph but wherever we have dependence.

```cpp
a and b are given
for(i = 0;i < m; i++) {
	degree[b]++;
}

for(i = 0; i <= N; i++) {
	if(degree[i] == 0)
		ind = i;
}

q.push(ind);
while(q.size() > 0) {
	int d = q.front();
	q.pop();
	cout << d << " ";
	arr.push(d);

	for(auto child: graph[d]) {
		degree[child]--;
		if(degree[child] == 0)
			q.push(child);
	}
}

if(arr.size() != N)
	# cycle exists
```

```cpp
#include <iostream>
#include <list>
#include <queue>
using namespace std;

void topologicalSort()
{
    vector<int> in_degree(V, 0);

    for (int v = 0; v < V; ++v) {
        for (auto const& w : adj[v])
            in_degree[w]++;
    }

    queue<int> q;
    for (int i = 0; i < V; ++i) {
        if (in_degree[i] == 0)
            q.push(i);
    }

    int count = 0;

    vector<int> top_order;

    while (!q.empty()) {
        int u = q.front();
        q.pop();
        top_order.push_back(u);

        list<int>::iterator itr;
        for (itr = adj[u].begin(); itr != adj[u].end();
             ++itr)
             
            if (--in_degree[*itr] == 0)
                q.push(*itr);

        count++;
    }

    if (count != V) {
        cout << "Graph contains cycle" << endl;
        return;
    }


    for (int i : top_order)
        cout << i << " ";
}
```

# Shortest Path Algorithms

### Dijkstra (imp)
No negative weights.
It calculates shortest distance from a node to all node.
O(n log n)
### Floyd `Warshall` (can skip this)
No negative weights.
It calculates distance from all nodes to all nodes.
O(N ^ 3)
### Bellman's Algorithm (can skip this)
When negative weights are given.
O(N^3)
# `DSU` (Disjoint Set Union) (imp)
It is not linked to graph.
Learn the union by size one.
# MST (Minimum Spanning Tree) (Prim's, `Kruskal`)
we implement it using `DSU`. 


