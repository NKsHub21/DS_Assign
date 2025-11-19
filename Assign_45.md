---


# <center> ASSIGNMENT NO - 5 Unit_5 </center>

## Title :

**Write a Program to accept a graph from a user and represent it with an Adjacency List and perform BFS and DFS traversals on it.**

---

## AIM

<p>To represent a graph using an adjacency list and perform BFS and DFS traversals starting from a given vertex.</p>

---

## OBJECTIVE

<p>Practice adjacency-list construction and traversal techniques to systematically visit all reachable vertices, analyzing levels (BFS) and depth exploration (DFS).</p>

---

## THEORY

<p>The adjacency list stores, for each vertex, a list of its neighbors. BFS explores vertices in layers using a queue, while DFS explores along a path as far as possible before backtracking, typically implemented via recursion.</p>

---

## ALGORITHM

1. Read number of vertices and edges.
2. Construct adjacency list for an undirected graph.
3. Input start vertex.
4. BFS: use a queue and visited array to process neighbors level-wise.
5. DFS: recursively explore unvisited neighbors depth-first.
6. Output orders of traversal.
7. End.

---

## CODE

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

void bfs_npk(const vector<vector<int>>& adj_npk, int start_npk) {
    int n_npk = adj_npk.size();
    vector<int> vis_npk(n_npk, 0);
    queue<int> q_npk;
    vis_npk[start_npk] = 1;
    q_npk.push(start_npk);
    cout << "BFS: ";
    while (!q_npk.empty()) {
        int u_npk = q_npk.front();
        q_npk.pop();
        cout << u_npk << " ";
        for (int v_npk : adj_npk[u_npk]) {
            if (!vis_npk[v_npk]) {
                vis_npk[v_npk] = 1;
                q_npk.push(v_npk);
            }
        }
    }
    cout << endl;
}

void dfsUtil_npk(const vector<vector<int>>& adj_npk, int u_npk, vector<int>& vis_npk) {
    vis_npk[u_npk] = 1;
    cout << u_npk << " ";
    for (int v_npk : adj_npk[u_npk]) {
        if (!vis_npk[v_npk]) dfsUtil_npk(adj_npk, v_npk, vis_npk);
    }
}

void dfs_npk(const vector<vector<int>>& adj_npk, int start_npk) {
    vector<int> vis_npk(adj_npk.size(), 0);
    cout << "DFS: ";
    dfsUtil_npk(adj_npk, start_npk, vis_npk);
    cout << endl;
}

int main_npk() {
    int n_npk, e_npk;
    cout << "Enter number of vertices and edges: ";
    cin >> n_npk >> e_npk;
    vector<vector<int>> adj_npk(n_npk);
    for (int i = 0; i < e_npk; i++) {
        int u_npk, v_npk;
        cin >> u_npk >> v_npk;
        adj_npk[u_npk].push_back(v_npk);
        adj_npk[v_npk].push_back(u_npk);
    }
    int start_npk;
    cout << "Enter start vertex: ";
    cin >> start_npk;

    bfs_npk(adj_npk, start_npk);
    dfs_npk(adj_npk, start_npk);
    return 0;
}

int main() {
    return main_npk();
}
```

---

## OUTPUT

```
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices and edges: 4 5
Enter edges (u v):
0 1
1 2
1 3
3 2
0 3
Enter start vertex: 0
BFS: 0 1 3 2 
DFS: 0 1 2 3
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>Adjacency list representation enabled efficient BFS and DFS traversals. BFS explored vertices by layers, while DFS explored along depth-first paths, demonstrating different visitation orders.</p>

---

