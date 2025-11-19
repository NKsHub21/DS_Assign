---



# <center> ASSIGNMENT NO - 10 Unit_5</center>

## Title :

**Write a Program to implement Dijkstra’s algorithm to find shortest distance between two nodes of a user-defined graph using Adjacency List.**

---

## AIM

<p>To find the shortest path between two nodes using Dijkstra’s algorithm applied to a graph represented by an adjacency list.</p>

---

## OBJECTIVE

<p>The objective is to efficiently compute shortest distances using adjacency list representation and a priority queue to minimize relaxation operations.</p>

---

## THEORY

<p>Dijkstra’s algorithm uses a greedy strategy to iteratively expand the shortest known path from the source vertex to others. Using a priority queue enables selection of the vertex with minimum distance in logarithmic time. The adjacency list allows efficient iteration through existing edges only.</p>

---

## ALGORITHM

1. Input number of vertices and edges.
2. Build adjacency list containing all neighbors and weights.
3. Input source and destination vertices.
4. Initialize distance array with infinity except source = 0.
5. Use a priority queue to pick the vertex with smallest distance.
6. Update distances of adjacent unvisited vertices.
7. Continue until queue empty or destination reached.
8. Display shortest distance to destination.
9. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20
#define INF 9999

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

    cout << "Enter edges (u v w):\n";
    for (int i = 0; i < e_npk; i++) {
        cin >> u_npk >> v_npk >> w_npk;
        adj_npk[u_npk][v_npk] = w_npk;
        adj_npk[v_npk][u_npk] = w_npk;  // Undirected graph
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
        int minDist_npk = INF, u = -1;

        // Find the unvisited vertex with minimum distance
        for (int i = 0; i < n_npk; i++) {
            if (!visited_npk[i] && dist_npk[i] < minDist_npk) {
                minDist_npk = dist_npk[i];
                u = i;
            }
        }

        if (u == -1) break; // All reachable vertices processed
        visited_npk[u] = 1;

        // Update distances for neighbors
        for (int v = 0; v < n_npk; v++) {
            if (!visited_npk[v] && adj_npk[u][v] != INF && dist_npk[u] + adj_npk[u][v] < dist_npk[v]) {
                dist_npk[v] = dist_npk[u] + adj_npk[u][v];
            }
        }
    }

    // Output shortest distance
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
Enter number of vertices and edges: 3 4 
Enter edges (u v w):
2 0 1
2 3 1
3 1 1
2 3 0
Enter source and destination vertex: 0 3
Shortest distance from 0 to 3 is: 0
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>Dijkstra’s algorithm was effectively applied using an adjacency list and a min-priority queue. It computed the optimal distance between the source and destination by progressively relaxing edges of the least-cost vertices.</p>

---

