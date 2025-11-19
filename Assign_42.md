---

##  File: `Unit-V_Assignment_2_Prim_AdjList.md`

# <center> ASSIGNMENT NO - 2 Unit_5 </center>

## Title :

**Write a Program to implement Prim’s algorithm to find the Minimum Spanning Tree (MST) of a user-defined graph using an Adjacency List.**

---

## AIM

<p>To apply Prim’s algorithm for finding the Minimum Spanning Tree of a connected weighted graph represented through an adjacency list.</p>

---

## OBJECTIVE

<p>The objective is to understand how Prim’s algorithm constructs a minimum-cost tree that connects all vertices by repeatedly selecting the minimum edge from a growing subset of vertices.</p>

---

## THEORY

<p><b>Prim’s algorithm</b> builds the MST starting from any vertex and repeatedly adds the smallest edge connecting a vertex inside the tree to a vertex outside it.  
An <b>adjacency list</b> represents the graph efficiently, storing each vertex’s neighbors and their edge weights.</p>

---

## ALGORITHM

1. Start.
2. Input number of vertices and edges.
3. Create adjacency list with edge weights.
4. Choose any vertex as the start.
5. Initialize key values to ∞ and include the starting vertex in the MST.
6. Pick the smallest key edge not yet in the MST.
7. Update keys of adjacent vertices.
8. Repeat until all vertices are included.
9. Display MST edges and total cost.
10. End.

---

## CODE

```cpp 
#include <iostream>
#include <vector>
#include <limits>
using namespace std;

int minKey_npk(vector<int>& key_npk, vector<bool>& mstSet_npk, int n_npk) {
    int min_npk = numeric_limits<int>::max(), index_npk = -1;
    for (int v_npk = 0; v_npk < n_npk; v_npk++) {
        if (!mstSet_npk[v_npk] && key_npk[v_npk] < min_npk) {
            min_npk = key_npk[v_npk];
            index_npk = v_npk;
        }
    }
    return index_npk;
}

void prim_npk(vector<vector<pair<int, int>>>& adj_npk, int n_npk) {
    vector<int> key_npk(n_npk, numeric_limits<int>::max());
    vector<int> parent_npk(n_npk, -1);
    vector<bool> mstSet_npk(n_npk, false);

    key_npk[0] = 0;
    for (int count = 0; count < n_npk - 1; count++) {
        int u_npk = minKey_npk(key_npk, mstSet_npk, n_npk);
        mstSet_npk[u_npk] = true;

        for (auto& it_npk : adj_npk[u_npk]) {
            int v_npk = it_npk.first;
            int w_npk = it_npk.second;
            if (!mstSet_npk[v_npk] && w_npk < key_npk[v_npk]) {
                parent_npk[v_npk] = u_npk;
                key_npk[v_npk] = w_npk;
            }
        }
    }

    int total_npk = 0;
    cout << "Edges in MST:\n";
    for (int i = 1; i < n_npk; i++) {
        cout << parent_npk[i] << " - " << i << endl;
        total_npk += key_npk[i];
    }
    cout << "Total cost: " << total_npk << endl;
}

int main_npk() {
    int n_npk, e_npk;
    cout << "Enter vertices and edges: ";
    cin >> n_npk >> e_npk;

    vector<vector<pair<int, int>>> adj_npk(n_npk);
    for (int i = 0; i < e_npk; i++) {
        int u_npk, v_npk, w_npk;
        cin >> u_npk >> v_npk >> w_npk;
        adj_npk[u_npk].push_back({v_npk, w_npk});
        adj_npk[v_npk].push_back({u_npk, w_npk});
    }

    prim_npk(adj_npk, n_npk);
    return 0;
}

int main() {
    return main_npk();
}
```

---

## OUTPUT

```
PS C:\Users\Nandini\Documents\DS_VIT> cd "c:\Users\Nandini\Documents\DS_VIT\" ; if ($?) { g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile } ; if ($?) { .\tempCodeRunnerFile }
Enter vertices and edges: 5 6
0 1 2
0 3 6
1 2 3
1 3 8
1 4 5
2 4 7
Edges in MST:
0 - 1
1 - 2
0 - 3
1 - 4
Total cost: 16
PS C:\Users\Nandini\Documents\DS_VIT> 
```

---

## CONCLUSION

<p>Prim’s algorithm was implemented using an adjacency list. The program efficiently determined the MST by repeatedly choosing the smallest weight edge connecting the growing tree to remaining vertices.</p>

---
