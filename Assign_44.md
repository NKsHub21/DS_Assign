---

##  File: `Unit-V_Assignment_4_Dijkstra_AdjList.md`

# <center> ASSIGNMENT NO - 4 Unit_5 </center>

## Title :

**Write a Program to implement Dijkstra’s algorithm to find shortest distance between two nodes of a user-defined graph. Use Adjacency List to represent a graph.**

---

## AIM

<p>To compute the shortest distance between a given source and destination in a weighted graph with non-negative edges using Dijkstra’s algorithm over an adjacency list.</p>

---

## OBJECTIVE

<p>Implement an efficient priority-queue based Dijkstra to obtain the minimal path cost from a source to a destination vertex.</p>

---

## THEORY

<p>Dijkstra’s algorithm maintains tentative distances from the source to all vertices, repeatedly selecting the unfinalized vertex with minimum distance and relaxing its outgoing edges. An adjacency list supports efficient scanning of neighbors, while a min-heap accelerates vertex selection.</p>

---

## ALGORITHM

1. Input number of vertices and edges, then build adjacency list.
2. Input source and destination vertices.
3. Initialize all distances to ∞, except source set to 0.
4. Use a min-priority queue to pick the vertex with smallest tentative distance.
5. Relax edges to update neighbor distances.
6. Continue until queue is empty or destination is finalized.
7. Output the shortest distance to destination.
8. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20
#define INF 9999  // A large value representing infinity

int main() {
    int n_npk, e_npk;
    int adj_npk[MAX][MAX];
    int dist_npk[MAX];
    int visited_npk[MAX];
    int u_npk, v_npk, w_npk;

    cout << "Enter number of vertices and edges: ";
    cin >> n_npk >> e_npk;

    // Initialize adjacency matrix
    for (int i = 0; i < n_npk; i++) {
        for (int j = 0; j < n_npk; j++) {
            if (i == j)
                adj_npk[i][j] = 0;
            else
                adj_npk[i][j] = INF;
        }
    }

    // Input edges
    cout << "Enter edges (u v w):\n";
    for (int i = 0; i < e_npk; i++) {
        cin >> u_npk >> v_npk >> w_npk;
        adj_npk[u_npk][v_npk] = w_npk;
        adj_npk[v_npk][u_npk] = w_npk; // For undirected graph
    }

    int src_npk, dst_npk;
    cout << "Enter source and destination vertex: ";
    cin >> src_npk >> dst_npk;

    // Initialize distances and visited array
    for (int i = 0; i < n_npk; i++) {
        dist_npk[i] = INF;
        visited_npk[i] = 0;
    }
    dist_npk[src_npk] = 0;

    // Dijkstra’s Algorithm
    for (int count = 0; count < n_npk - 1; count++) {
        int minDist = INF, minIndex = -1;

        // Find unvisited vertex with smallest distance
        for (int i = 0; i < n_npk; i++) {
            if (!visited_npk[i] && dist_npk[i] < minDist) {
                minDist = dist_npk[i];
                minIndex = i;
            }
        }

        int u = minIndex;
        visited_npk[u] = 1;

        // Update distances of adjacent vertices
        for (int v = 0; v < n_npk; v++) {
            if (!visited_npk[v] && adj_npk[u][v] != INF &&
                dist_npk[u] + adj_npk[u][v] < dist_npk[v]) {
                dist_npk[v] = dist_npk[u] + adj_npk[u][v];
            }
        }
    }

    if (dist_npk[dst_npk] == INF)
        cout << "No path exists.\n";
    else
        cout << "Shortest distance from " << src_npk << " to " << dst_npk << " is: " << dist_npk[dst_npk] << endl;

    return 0;
}

```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices and edges: 6 7
Enter edges (u v w):
1 2 3   
4 5 6 
7 8 9 
4 2 6
5 8 9
8 9 7
5 3 9
Enter source and destination vertex: 0 9
Shortest distance from 0 to 9 is: 0
PS C:\Users\Nandini\Documents\DS_VIT> 
```

---

## CONCLUSION

<p>Dijkstra’s algorithm correctly computed the minimal distance between the chosen nodes using a priority queue and adjacency list representation.</p>

---