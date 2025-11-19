---



# <center> ASSIGNMENT NO - 7 Unit_5 </center>

## Title :

**Write a Program to implement Dijkstra’s algorithm to find shortest distance between two nodes of a user-defined graph using Adjacency Matrix.**

---

## AIM

<p>To find the shortest path between two nodes using Dijkstra’s algorithm on a weighted graph represented by an adjacency matrix.</p>

---

## OBJECTIVE

<p>The goal is to understand how Dijkstra’s algorithm efficiently computes minimal distances by updating tentative distances for all neighbors of each selected vertex using adjacency matrix scanning.</p>

---

## THEORY

<p>Dijkstra’s algorithm computes the shortest path from a source vertex to all others in a graph with non-negative edge weights. The adjacency matrix provides direct access to edge weights for all vertex pairs. The vertex with the smallest temporary distance is finalized at each step.</p>

---

## ALGORITHM

1. Start.
2. Input adjacency matrix and source vertex.
3. Initialize distance array with infinity; distance of source = 0.
4. Repeat for all vertices:

   * Pick vertex with smallest temporary distance not yet visited.
   * Update distances of its adjacent vertices.
5. Stop when all vertices processed.
6. Output final distances.
7. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20
#define INF 9999  // A large number representing infinity

void dijkstra_npk(int adj_npk[MAX][MAX], int n_npk, int src_npk) {
    int dist_npk[MAX];     // Stores shortest distances
    int visited_npk[MAX];  // Marks visited vertices

    // Initialize distances and visited array
    for (int i = 0; i < n_npk; i++) {
        dist_npk[i] = INF;
        visited_npk[i] = 0;
    }
    dist_npk[src_npk] = 0;

    // Dijkstra's Algorithm main loop
    for (int count = 0; count < n_npk - 1; count++) {
        int minDist = INF, u_npk = -1;

        // Find the vertex with minimum distance that is not visited
        for (int i = 0; i < n_npk; i++) {
            if (!visited_npk[i] && dist_npk[i] < minDist) {
                minDist = dist_npk[i];
                u_npk = i;
            }
        }

        visited_npk[u_npk] = 1;

        // Update distances of adjacent vertices
        for (int v_npk = 0; v_npk < n_npk; v_npk++) {
            if (!visited_npk[v_npk] && adj_npk[u_npk][v_npk] != 0 &&
                dist_npk[u_npk] + adj_npk[u_npk][v_npk] < dist_npk[v_npk]) {
                dist_npk[v_npk] = dist_npk[u_npk] + adj_npk[u_npk][v_npk];
            }
        }
    }

    // Output results
    cout << "\nShortest distances from vertex " << src_npk << ":\n";
    for (int i = 0; i < n_npk; i++) {
        if (dist_npk[i] == INF)
            cout << src_npk << " -> " << i << " = No Path\n";
        else
            cout << src_npk << " -> " << i << " = " << dist_npk[i] << endl;
    }
}

int main() {
    int n_npk;
    int adj_npk[MAX][MAX];
    int src_npk;

    cout << "Enter number of vertices: ";
    cin >> n_npk;

    cout << "Enter adjacency matrix (0 if no edge):\n";
    for (int i = 0; i < n_npk; i++) {
        for (int j = 0; j < n_npk; j++) {
            cin >> adj_npk[i][j];
        }
    }

    cout << "Enter source vertex: ";
    cin >> src_npk;

    dijkstra_npk(adj_npk, n_npk, src_npk);

    return 0;
}

```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices: 3
Enter adjacency matrix (0 for no edge):
1 2 3
5 3 1
4 5 2
Edges in MST:
1 - 2 (1)
0 - 1 (2)
Total cost of MST: 3
Enter number of vertices: 3
Enter adjacency matrix (0 for no edge):
1 2 3
5 3 1
4 5 2
Edges in MST:
1 - 2 (1)
0 - 1 (2)
1 2 3
5 3 1
4 5 2
Edges in MST:
1 - 2 (1)
0 - 1 (2)
4 5 2
Edges in MST:
1 - 2 (1)
0 - 1 (2)
0 - 1 (2)
Total cost of MST: 3
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices: 3
Enter adjacency matrix (0 if no edge):
1 2 3
3 0 1
2 3 0
Enter source vertex: 0

Shortest distances from vertex 0:
0 -> 0 = 0
0 -> 1 = 2
0 -> 2 = 3
PS C:\Users\Nandini\Documents\DS_VIT> 

```

---

## CONCLUSION

<p>Dijkstra’s algorithm was applied successfully using an adjacency matrix. It computed minimal distances from the source vertex by iteratively updating shortest paths to adjacent vertices.</p>

---

