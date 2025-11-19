
---

##  File: `Unit-V_Assignment_3_Kruskal_AdjList.md`

# <center> ASSIGNMENT NO - 3 Unit_5</center>

## Title :

**Write a Program to implement Kruskal’s algorithm to find the Minimum Spanning Tree (MST) of a user-defined graph. Use Adjacency List to represent a graph.**

---

## AIM

<p>To construct the Minimum Spanning Tree of a connected, weighted, undirected graph using Kruskal’s algorithm with an adjacency list representation.</p>

---

## OBJECTIVE

<p>Implement Kruskal’s algorithm by sorting edges by weight and using a disjoint-set union (DSU) structure to avoid cycles, thereby selecting edges of minimum cost to connect all vertices.</p>

---

## THEORY

<p>Kruskal’s algorithm considers all edges in non-decreasing order of weight, adding an edge to the MST if it does not create a cycle. Cycle detection and component merging are performed by a DSU (Union–Find). For adjacency lists, the edge list can be constructed by iterating neighbors and capturing unique undirected edges once.</p>

---

## ALGORITHM

1. Input number of vertices and edges.
2. Build an adjacency list storing neighbors and weights.
3. Convert adjacency list to an edge list without duplicates.
4. Sort edges by weight ascending.
5. Initialize DSU for all vertices.
6. For each edge in sorted order, if endpoints are in different sets, include it in MST and union the sets.
7. Print MST edges and total cost.
8. End.

---

## CODE

```cpp
#include <iostream>
using namespace std;

#define MAX 50  


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
    int n_npk, e_npk;
    cout << "Enter number of vertices and edges: ";
    cin >> n_npk >> e_npk;

    int u_npk[MAX], v_npk[MAX], w_npk[MAX];

    cout << "Enter edges (u v w):\n";
    for (int i = 0; i < e_npk; i++) {
        cin >> u_npk[i] >> v_npk[i] >> w_npk[i];
    }

    for (int i = 0; i < e_npk - 1; i++) {
        for (int j = 0; j < e_npk - i - 1; j++) {
            if (w_npk[j] > w_npk[j + 1]) {
                int temp;
                // Swap weights
                temp = w_npk[j]; w_npk[j] = w_npk[j + 1]; w_npk[j + 1] = temp;
                // Swap vertices
                temp = u_npk[j]; u_npk[j] = u_npk[j + 1]; u_npk[j + 1] = temp;
                temp = v_npk[j]; v_npk[j] = v_npk[j + 1]; v_npk[j + 1] = temp;
            }
        }
    }

    
    DSU_npk dsu_npk;
    dsu_npk.makeSet_npk(n_npk);

    int total_npk = 0, used_npk = 0;
    cout << "\nEdges in Minimum Spanning Tree:\n";

    for (int i = 0; i < e_npk && used_npk < n_npk - 1; i++) {
        if (dsu_npk.unite_npk(u_npk[i], v_npk[i])) {
            cout << u_npk[i] << " - " << v_npk[i] << " (" << w_npk[i] << ")\n";
            total_npk += w_npk[i];
            used_npk++;
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
Enter number of vertices and edges: 5 7
Enter edges (u v w):
0 1 2
0 3 6
1 2 3
1 3 8
1 4 5
2 4 7
3 4 9

Edges in Minimum Spanning Tree:
0 - 1 (2)
1 - 2 (3)
1 - 4 (5)
0 - 3 (6)
Total cost of MST: 16
PS C:\Users\Nandini\Documents\DS_VIT> 
```

---

## CONCLUSION

<p>Kruskal’s algorithm using DSU produced the MST by selecting the smallest edges that do not form cycles. The adjacency list was converted to a unique edge list for sorting and processing.</p>

---



