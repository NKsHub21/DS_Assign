



# <center> ASSIGNMENT NO - 6 Unit_5 </center>

## Title :

**Write a Program to implement Kruskal’s algorithm to find the Minimum Spanning Tree (MST) of a user-defined graph using an Adjacency Matrix.**

---

## AIM

<p>To design and implement Kruskal’s algorithm to find the Minimum Spanning Tree (MST) for a connected weighted graph represented by an adjacency matrix.</p>

---

## OBJECTIVE

<p>The objective is to construct a Minimum Spanning Tree using Kruskal’s algorithm that connects all vertices with minimal total edge cost, avoiding cycles through a union–find structure.</p>

---

## THEORY

<p><b>Kruskal’s algorithm</b> is a greedy algorithm that sorts all edges of a weighted graph in increasing order of weights and includes them in the MST if they do not form a cycle. Cycle detection is handled by a <b>Disjoint Set Union (DSU)</b> or <b>Union-Find</b> data structure.  
An <b>Adjacency Matrix</b> representation allows easy retrieval of all edges by iterating through matrix entries.</p>

---

## ALGORITHM

1. Start.
2. Input number of vertices and adjacency matrix.
3. Store all edges `(u, v, w)` in an edge list (for non-zero weights).
4. Sort the edges by weight.
5. Initialize DSU for all vertices.
6. Add edges one by one to MST if they connect disjoint components.
7. Continue until (V−1) edges are included.
8. Display MST and total cost.
9. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 20
#define INF 9999

struct DSU_npk {
    int parent_npk[MAX];
    int rank_npk[MAX];

    void makeSet_npk(int n_npk) {
        for (int i = 0; i < n_npk; i++) {
            parent_npk[i] = i;
            rank_npk[i] = 0;
        }
    }

    int find_npk(int x_npk) {
        if (parent_npk[x_npk] != x_npk)
            parent_npk[x_npk] = find_npk(parent_npk[x_npk]);
        return parent_npk[x_npk];
    }

    bool unite_npk(int a_npk, int b_npk) {
        a_npk = find_npk(a_npk);
        b_npk = find_npk(b_npk);
        if (a_npk == b_npk) return false;

        if (rank_npk[a_npk] < rank_npk[b_npk])
            parent_npk[a_npk] = b_npk;
        else if (rank_npk[a_npk] > rank_npk[b_npk])
            parent_npk[b_npk] = a_npk;
        else {
            parent_npk[b_npk] = a_npk;
            rank_npk[a_npk]++;
        }
        return true;
    }
};

int main() {
    int n_npk;
    int adj_npk[MAX][MAX];
    int edges_npk[MAX * MAX][3]; // [weight, u, v]
    int edgeCount_npk = 0;

    cout << "Enter number of vertices: ";
    cin >> n_npk;

    cout << "Enter adjacency matrix (0 for no edge):\n";
    for (int i = 0; i < n_npk; i++) {
        for (int j = 0; j < n_npk; j++) {
            cin >> adj_npk[i][j];
            if (j > i && adj_npk[i][j] != 0) {
                edges_npk[edgeCount_npk][0] = adj_npk[i][j]; // weight
                edges_npk[edgeCount_npk][1] = i;             // u
                edges_npk[edgeCount_npk][2] = j;             // v
                edgeCount_npk++;
            }
        }
    }

    // Sort edges by weight (Bubble Sort)
    for (int i = 0; i < edgeCount_npk - 1; i++) {
        for (int j = 0; j < edgeCount_npk - i - 1; j++) {
            if (edges_npk[j][0] > edges_npk[j + 1][0]) {
                int temp;
                for (int k = 0; k < 3; k++) {
                    temp = edges_npk[j][k];
                    edges_npk[j][k] = edges_npk[j + 1][k];
                    edges_npk[j + 1][k] = temp;
                }
            }
        }
    }

    DSU_npk dsu_npk;
    dsu_npk.makeSet_npk(n_npk);

    int total_npk = 0;
    cout << "Edges in MST:\n";
    for (int i = 0; i < edgeCount_npk; i++) {
        int w_npk = edges_npk[i][0];
        int u_npk = edges_npk[i][1];
        int v_npk = edges_npk[i][2];
        if (dsu_npk.unite_npk(u_npk, v_npk)) {
            cout << u_npk << " - " << v_npk << " (" << w_npk << ")\n";
            total_npk += w_npk;
        }
    }

    cout << "Total cost of MST: " << total_npk << endl;
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
PS C:\Users\Nandini\Documents\DS_VIT> w
```

---

## CONCLUSION

<p>Kruskal’s algorithm successfully found the minimum spanning tree from the adjacency matrix by selecting edges in increasing weight order and avoiding cycles using DSU.</p>

---

