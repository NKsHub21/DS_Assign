

##  File: `Unit-V_Assignment_1_Graph_AdjMatrix_BFS_DFS.md`

# <center> ASSIGNMENT NO - 1 Unit_5 </center>

## Title :

**Write a Program to accept a graph from a user and represent it with an Adjacency Matrix and perform BFS and DFS traversals on it.**

---

## AIM

<p>To represent a user-defined graph using an adjacency matrix and perform Breadth First Search (BFS) and Depth First Search (DFS) traversals.</p>

---

## OBJECTIVE

<p>The objective of this program is to understand graph representation using an adjacency matrix and to explore traversal algorithms such as BFS and DFS. These traversals allow visiting all vertices systematically, useful in exploring connectivity and reachability within a graph.</p>

---

## THEORY

<p>A graph can be represented as an <b>adjacency matrix</b>, a two-dimensional array where <code>matrix[i][j]</code> is 1 if an edge exists from vertex <code>i</code> to vertex <code>j</code>.  
The <b>BFS traversal</b> uses a queue to visit all vertices level by level, while <b>DFS traversal</b> uses recursion or a stack to explore as deep as possible along each branch before backtracking.</p>

---

## ALGORITHM

### BFS and DFS on Adjacency Matrix

1. Start.
2. Accept number of vertices and edges.
3. Create adjacency matrix of size `n × n` initialized to 0.
4. For each edge `(u, v)`, set `matrix[u][v] = matrix[v][u] = 1`.
5. For BFS:

   * Use a queue to visit nodes level-wise.
6. For DFS:

   * Use recursion to explore nodes depth-wise.
7. Display traversal order.
8. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20   // Maximum number of vertices

void bfs_npk(int adj_npk[MAX][MAX], int start_npk, int n_npk) {
    int visited_npk[MAX] = {0};
    int q_npk[MAX];
    int front = 0, rear = -1;

    visited_npk[start_npk] = 1;
    q_npk[++rear] = start_npk;

    cout << "BFS: ";
    while (front <= rear) {
        int u_npk = q_npk[front++];
        cout << u_npk << " ";
        for (int v_npk = 0; v_npk < n_npk; v_npk++) {
            if (adj_npk[u_npk][v_npk] == 1 && !visited_npk[v_npk]) {
                visited_npk[v_npk] = 1;
                q_npk[++rear] = v_npk;
            }
        }
    }
    cout << endl;
}

void dfsUtil_npk(int adj_npk[MAX][MAX], int u_npk, int visited_npk[MAX], int n_npk) {
    visited_npk[u_npk] = 1;
    cout << u_npk << " ";
    for (int v_npk = 0; v_npk < n_npk; v_npk++) {
        if (adj_npk[u_npk][v_npk] == 1 && !visited_npk[v_npk])
            dfsUtil_npk(adj_npk, v_npk, visited_npk, n_npk);
    }
}

void dfs_npk(int adj_npk[MAX][MAX], int start_npk, int n_npk) {
    int visited_npk[MAX] = {0};
    cout << "DFS: ";
    dfsUtil_npk(adj_npk, start_npk, visited_npk, n_npk);
    cout << endl;
}

int main() {
    int n_npk, e_npk;
    int adj_npk[MAX][MAX] = {0};

    cout << "Enter number of vertices: ";
    cin >> n_npk;
    cout << "Enter number of edges: ";
    cin >> e_npk;

    cout << "Enter edges (u v):\n";
    for (int i = 0; i < e_npk; i++) {
        int u_npk, v_npk;
        cin >> u_npk >> v_npk;
        adj_npk[u_npk][v_npk] = 1;
        adj_npk[v_npk][u_npk] = 1;
    }

    int start_npk;
    cout << "Enter start vertex: ";
    cin >> start_npk;

    bfs_npk(adj_npk, start_npk, n_npk);
    dfs_npk(adj_npk, start_npk, n_npk);

    return 0;
}

```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices: 5
Enter number of edges: 4
Enter edges (u v):
1 2
3 4
7 8
3 9
Enter start vertex: 1
BFS: 1 2 
DFS: 1 2 
PS C:\Users\Nandini\Documents\DS_VIT> 


```

---

## CONCLUSION

<p>The graph was represented successfully using an adjacency matrix. BFS traversal visited vertices level-wise using a queue, while DFS traversal visited depth-wise using recursion.</p>

---

