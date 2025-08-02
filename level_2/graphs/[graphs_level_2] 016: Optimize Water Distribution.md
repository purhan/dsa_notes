# Problem Statement

There are n construction sites in a town. We want to supply water for all the construction sites by building wells and laying pipes.

For each site i, we can either build a well inside it directly with cost wells[i-1], or pipe in water from another well to it. The costs to lay pipes between
sites are given by the 2d array cost, where each row of cost contains 3 numbers ai,bi and wi where wi is the cost to connect ai to bi. connections are bidirectional.

Return the minimum total cost to supply water to all the construction sites.

[Tutorial](https://www.youtube.com/watch?v=gc6ShDTldb4&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=32)

# Thought Process
- We have to create a network of water supply. The only source of water initially is a well anywhere in the network.
- For each edge, we can either dig a well there, or pipe it with another site that already has water coming.
- This is a simple implementation of MST using prim or kruskal (prim's is used here)
- We create an edge for each town to the well and give it a weight of cost of well at that site
- We finally find out the total cost of MST and that is the answer

# Code
```cpp
int n, e;
vector<vector<pair<int, int>>> graph;
vector<int> wells;

class Compare {
public:
    bool operator() (const pair<int, int>& a, const pair<int, int>& b)
    {
        return a.second > b.second;
    }
};

void solve() {

    // add all wells as edges
    for (int i = 1; i <= n; ++i) {
        graph[i].push_back({0, wells[i - 1]});
        graph[0].push_back({i, wells[i - 1]});
    }

    // perform prims algo from here
    vector<bool> visited(n + 1);
    int ans = 0;
    priority_queue<pair<int, int>, vector<pair<int, int>>, Compare> pq;
    pq.push({0, 0});

    while (!pq.empty()) {
        auto best = pq.top();
        pq.pop();

        int src = best.first;
        int weight = best.second;

        if (visited[src]) continue;
        visited[src] = true;
        ans += weight;

        auto nbrs = graph[src];

        for (auto nbr : nbrs) {
            if (!visited[nbr.first])
                pq.push(nbr);
        }
    }

    cout << ans;
}

int main() {
    cin >> n >> e;
    wells = vector<int>(n);
    graph = vector<vector<pair<int, int>>>(n + 1);
    for (int i = 0; i < n; ++i) cin >> wells[i];

    int u, v, wt;
    for (int i = 0; i < e; ++i) {
        cin >> u >> v >> wt;
        graph[u].push_back({v, wt});
        graph[v].push_back({u, wt});
    }

    solve();

    return 0;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/optimize-water-distribution-official/ojquestion
