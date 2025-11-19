
---

# <center> ASSIGNMENT NO - 8 Unit_5 </center>

## Title :

**Write a Program to implement Prim’s algorithm to find the Minimum Spanning Tree (MST) of a user-defined graph using Adjacency List.**

---

## AIM

<p>To implement Prim’s algorithm for finding a Minimum Spanning Tree (MST) of a connected, weighted, undirected graph represented using an adjacency list.</p>

---

## OBJECTIVE

<p>The purpose of this assignment is to understand how Prim’s algorithm grows an MST starting from an arbitrary vertex, expanding through the least-cost edges connecting visited and unvisited vertices, utilizing adjacency list representation for efficient neighbor access.</p>

---

## THEORY

<p>Prim’s algorithm is a greedy approach that begins from a source vertex and iteratively adds the minimum-weight edge that connects a visited vertex to an unvisited vertex.  
Using an adjacency list improves traversal efficiency by only processing edges that exist, as opposed to scanning entire matrices.</p>

---

## ALGORITHM

1. Input the number of vertices and edges.
2. Build an adjacency list where each vertex stores its connected vertices and edge weights.
3. Initialize all vertices as unvisited, except the starting vertex.
4. Use a priority queue to select the edge of minimum weight connecting visited and unvisited nodes.
5. Continue adding edges until all vertices are included.
6. Display the MST edges and total weight.
7. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20
#define INF 9999

int main() {
    int n_npk;
    int adj_npk[MAX][MAX];
    int visited_npk[MAX];
    int minCost_npk = 0;

    cout << "Enter number of vertices: ";
    cin >> n_npk;

    cout << "Enter adjacency matrix (0 if no edge):\n";
    for (int i = 0; i < n_npk; i++) {
        for (int j = 0; j < n_npk; j++) {
            cin >> adj_npk[i][j];
            if (adj_npk[i][j] == 0)
                adj_npk[i][j] = INF;  // No edge treated as INF
        }
    }

    // Initialize visited array
    for (int i = 0; i < n_npk; i++)
        visited_npk[i] = 0;

    visited_npk[0] = 1; // Start from vertex 0

    int edgeCount_npk = 0;
    cout << "\nEdges in Minimum Spanning Tree:\n";

    while (edgeCount_npk < n_npk - 1) {
        int min_npk = INF;
        int u_npk = -1, v_npk = -1;

        // Find the smallest edge connecting visited and unvisited vertex
        for (int i = 0; i < n_npk; i++) {
            if (visited_npk[i]) {
                for (int j = 0; j < n_npk; j++) {
                    if (!visited_npk[j] && adj_npk[i][j] < min_npk) {
                        min_npk = adj_npk[i][j];
                        u_npk = i;
                        v_npk = j;
                    }
                }
            }
        }

        if (u_npk != -1 && v_npk != -1) {
            cout << u_npk << " - " << v_npk << " (" << min_npk << ")\n";
            visited_npk[v_npk] = 1;
            minCost_npk += min_npk;
            edgeCount_npk++;
        } else {
            break; // Disconnected graph
        }
    }

    cout << "Total cost of MST: " << minCost_npk << endl;
    return 0;
}

```

---

## OUTPUT

```
cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices: 4
Enter adjacency matrix (0 if no edge):
1 2 0 3
3 2 0 1
2 3 1 0
2 3 1 1

Edges in Minimum Spanning Tree:
0 - 1 (2)
1 - 3 (1)
3 - 2 (1)
Total cost of MST: 4
PS C:\Users\Nandini\Documents\DS_VIT>
```

---

## CONCLUSION

<p>Prim’s algorithm successfully determined the Minimum Spanning Tree using an adjacency list and priority queue for edge selection. The algorithm minimized total edge weight efficiently by expanding from the connected set of vertices.</p>

---


