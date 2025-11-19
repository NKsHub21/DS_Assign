---
# <center> ASSIGNMENT NO - 9 Unit_5 </center>

## Title :

**Write a Program to implement Kruskal’s algorithm to find the Minimum Spanning Tree (MST) of a user-defined graph using Adjacency List.**

---

## AIM

<p>To apply Kruskal’s algorithm to determine the Minimum Spanning Tree of a weighted graph using adjacency list representation.</p>

---

## OBJECTIVE

<p>To understand edge-based greedy selection in constructing MST by sorting edges and preventing cycles with Disjoint Set Union (DSU) operations.</p>

---

## THEORY

<p>Kruskal’s algorithm is an edge-centric method. It collects all edges, sorts them by weight, and iteratively adds the smallest non-cyclic edge to the MST.  
Cycle prevention is handled via Union–Find operations, and adjacency lists help efficiently store and retrieve edge data.</p>

---

## ALGORITHM

1. Input the number of vertices and edges.
2. Store all edges `(u, v, w)` in an edge list.
3. Sort edges by ascending weights.
4. Initialize DSU for all vertices.
5. For each edge, if it connects different components, include it in MST.
6. Stop after (V–1) edges are selected.
7. Display the MST edges and total weight.
8. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 50

// ---------- Disjoint Set Union (Union-Find) ----------
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
        if (a_npk == b_npk)
            return false;

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

// ---------- Main Kruskal Implementation ----------
int main() {
    int n_npk, e_npk;
    int edges_npk[MAX][3]; // Each edge: [weight, u, v]

    cout << "Enter number of vertices and edges: ";
    cin >> n_npk >> e_npk;

    cout << "Enter edges (u v w):\n";
    for (int i = 0; i < e_npk; i++) {
        cin >> edges_npk[i][1] >> edges_npk[i][2] >> edges_npk[i][0]; // Store as w,u,v
    }

    // ---------- Sort edges by weight (Bubble Sort) ----------
    for (int i = 0; i < e_npk - 1; i++) {
        for (int j = 0; j < e_npk - i - 1; j++) {
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

    // ---------- Kruskal’s Algorithm ----------
    DSU_npk dsu_npk;
    dsu_npk.makeSet_npk(n_npk);

    int total_npk = 0;
    cout << "\nEdges in MST:\n";
    for (int i = 0; i < e_npk; i++) {
        int w_npk = edges_npk[i][0];
        int u_npk = edges_npk[i][1];
        int v_npk = edges_npk[i][2];

        if (dsu_npk.unite_npk(u_npk, v_npk)) {
            cout << u_npk << " - " << v_npk << " (" << w_npk << ")\n";
            total_npk += w_npk;
        }
    }

    cout << "Total cost: " << total_npk << endl;
    return 0;
}

```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter number of vertices and edges: 4 4
Enter edges (u v w):
1 0 3
1 2 3
2 0 1
3 0 2

Edges in MST:
2 - 0 (1)
3 - 0 (2)
1 - 0 (3)
Total cost: 6
PS C:\Users\Nandini\Documents\DS_VIT> 

```

---

## CONCLUSION

<p>Kruskal’s algorithm efficiently generated the MST by processing edges sorted by weight. The adjacency list representation allowed straightforward edge handling, and DSU ensured cycle-free construction.</p>

---
