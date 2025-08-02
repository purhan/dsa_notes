# Problem Statement

Given a Directed Graph, find a Mother Vertex in the Graph (if present).
A Mother Vertex is a vertex through which we can reach all the other vertices of the Graph.

[Tutorial]()

# Thought Process
- Similar to Kosaraju
- Create a stack
- Do a DFS from any vertex, add to stack while backtracking
- The last item in the stack (or top) at the end of this, can be a mother vertex
- Run a DFS from this vertex to confirm this is a mother vertex. Else, no mother vertex exists.

# Code
```cpp
void dfs_(vector<vector<int>> &graph, int src, vector<bool> &vis) {
    if (vis[src]) return;
    vis[src] = true;
    for (int i : graph[src]) {
        dfs_(graph, i, vis);
    }
}

void dfs(vector<vector<int>> &graph, int src, vector<bool> &vis, stack<int>&st) {
    if (vis[src]) return;
    vis[src] = true;
    for (int i : graph[src]) {
        dfs(graph, i, vis, st);
    }
    st.push(src);
}

void findMotherVertex(int n, vector<vector<int>> &graph) {
    stack<int> st;

    vector<bool> vis(n + 1, false);

    for (int i = 0; i < n; i++) {
        if (!vis[i]) {
            dfs(graph, i, vis, st);
        }
    }

    vector<bool> nvis(n + 1, false);
    vis = nvis;

    int node = st.top();
    dfs_(graph, node, vis);

    for (int i = 0; i < n; i++) {
        if (vis[i] == false) {
            cout << -1;
            return;
        }
    }

    cout << node + 1 << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/mother-vertex-official/ojquestion
