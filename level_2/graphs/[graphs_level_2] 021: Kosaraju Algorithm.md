# Problem Statement

You are given a graph with N nodes and M directed edges. Find the number of Strongly connected components in the graph.

[Tutorial](https://www.youtube.com/watch?v=QtdE7QPsWiU&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=21)

# Thought Process
- Create a stack
- First, do a random order DFS and add to stack WHILE BACKTRACKING
- Once all the nodes are visited, reverse all the edges, and do a DFS on all the nodes
- If ever encountered an unvisited node after this DFS, add 1 to the answer, and continue DFS from this node

![image](https://user-images.githubusercontent.com/10897423/143884322-f4ceefb9-6443-4a1d-bf0f-59c6ab5f5b2f.png)

Striver's Explanation
- Do a Topological sort (that stack we created, and then pushed while backtracking, all that is just topological sort)
- Reverse the graph
- Do a DFS over the reversed graph (do it in the order obtained from topological sort)
- Connected components of this DFS will give us strongly connected component

# Code

Striver's Code:

```cpp
class Solution
{
    void dfs(stack<int>& st, vector<bool>& visited, vector<int> adj[], int i) {
        if(visited[i]) return;
        visited[i] = true;
        for(auto k: adj[i]) {
            dfs(st, visited, adj, k);
        }
        st.push(i);
    }

public:
    int kosaraju(int V, vector<int> adj[])
    {
        // Do a topological sort
        // - create a stack
        // - push into stack while backtracking from dfs
        stack<int> st, st1; // dont mind the second stack, its useless
        vector<bool>visited(V);
        for(int i = 0; i < V; ++i) {
            if(!visited[i]) dfs(st, visited, adj, i);
        }

        // Reverse the graph
        vector<int> reverse[V];
        for(int i = 0; i < V; ++i) {
            visited[i] = false;
            for(auto k: adj[i]) {
                reverse[k].push_back(i);
            }
        }

        // Run DFS on reversed graph. Connected components for this, is the ans
        int scc = 0;
        while(!st.empty()) {
            int node = st.top(); st.pop();
            if(!visited[node]) {
                scc++;
                dfs(st1, visited, reverse, node);
            }
        }
        return scc;
    }
};
```

Pepcoding's Code:

```cpp
void dfs(vector<vector<int>> &graph, int src, stack<int> &st, vector<bool> &vis)
{
    vis[src] = true;
    for (int vtx : graph[src])
    {
        if (vis[vtx] == false)
        {
            dfs(graph, vtx, st, vis);
        }
    }

    st.push(src);
}

void dfs_(vector<vector<int>> &graph, int src, vector<bool> &vis)
{
    vis[src] = true;
    for (int vtx : graph[src])
    {
        if (vis[vtx] == false)
        {
            dfs_(graph, vtx, vis);
        }
    }
}

int stronglyConnectedComponents(vector<vector<int>> &graph)
{
    int v = graph.size();
    vector<bool> vis(v, false);
    stack<int> st;

    // store all the nodes
    for (int i = 0; i < v; i++)
    {
        if (vis[i] == false)
        {
            dfs(graph, i, st, vis);
        }
    }

    // reverse all the edges
    vector<vector<int>> revgraph(v, vector<int>());

    for (int i = 0; i < v; i++)
    {
        for (int j = 0; j < graph[i].size(); j++)
        {
            int src = i;
            int nbr = graph[i][j];

            revgraph[nbr].push_back(src);
        }
    }

    // count the scc(dfs) using stack
    int scc = 0;
    vector<bool> nvis(v, false);

    while (st.size() > 0)
    {
        int top = st.top();
        st.pop();
        if (nvis[top] == false)
        {
            dfs_(revgraph, top, nvis);
            scc++;
        }
    }

    return scc;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/kosaraju-algorithm-official/ojquestion#!
