1. Directed edge (one way)
2. Non-directed edge (bi-directional)

## Cyclic graph.
- Graphs have cycles while trees do not.
- If no. of edges is equal to node - 1 then there is no cycle (meaning it is a tree)

1. Connected Graph:- All nodes are connected.
2. Dis-connected Graph:- All nodes are not connected.

1. Adjacency Matrix: We make n * n matrix and corresponding to each value, we make it 1 if there is a connection otherwise 0. Space O(N^2)
2. Adjacency List: Mostly we use list because it takes less space than matrix. Corresponding to each element in the graph we have a vector or LL of all the nodes connected to it. So `vector<LL> or vector<vecotr<int>>`. Space O(N + E).

## `DFS`
```cpp
#include <bits/stdc++.h>
using namespace std;

class Graph {
public:
    map<int, bool> visited;
    map<int, list<int> > adj;

    void addEdge(int v, int w);

    void DFS(int v);
};

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
}

void Graph::DFS(int v)
{
    visited[v] = true;
    cout << v << " ";

    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFS(*i);
}

int main()
{
    Graph g;
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);

    cout << "Following is Depth First Traversal"
            " (starting from vertex 2) \n";

    g.DFS(2);

    return 0;
}
```

## `BFS`
```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void bfs(vector<vector<int> >& adjList, int startNode,
         vector<bool>& visited)
{
    queue<int> q;

    visited[startNode] = true;
    q.push(startNode);

    while (!q.empty()) {
        int currentNode = q.front();
        q.pop();
        cout << currentNode << " ";

        for (int neighbor : adjList[currentNode]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

void addEdge(vector<vector<int> >& adjList, int u, int v)
{
    adjList[u].push_back(v);
}

int main()
{
    int vertices = 5;

    vector<vector<int> > adjList(vertices);

    addEdge(adjList, 0, 1);
    addEdge(adjList, 0, 2);
    addEdge(adjList, 1, 3);
    addEdge(adjList, 1, 4);
    addEdge(adjList, 2, 4);

    vector<bool> visited(vertices, false);

    cout << "Breadth First Traversal starting from vertex "
            "0: ";
    bfs(adjList, 0, visited);

    return 0;
}
```

## Find The Number Of Islands (`GFG`)

## Undirected Graph Cycle

## 