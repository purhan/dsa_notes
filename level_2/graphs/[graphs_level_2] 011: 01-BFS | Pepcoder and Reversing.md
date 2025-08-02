# Problem Statement
You are given 2 integers N and M , N is the number of vertices, M is the number of edges. You'll also be given ai and bi where ai and bi represents an edge from a vertex ai to a vertex bi.

You have to find the minimum number of edges you have to reverse in order to have atleast one path from vertex 1 to N, where the vertices are numbered from 1 to N.

[Tutorial](https://www.youtube.com/watch?v=Xqq7uELiYnE&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=11)

# Thought Process
- We can add all paths with weight 0, additionally, we will add reverse of all paths and give each a weight of 1
- We can then run dijkstra over it to find the shortest path with min cost, min cost is the answer

To run dijkstra:
- We use a priority queue
- We add smaller weights in higher priority and heavier weights in lower priority
- We process all vertices from the pq and add their neighbors to the pq. While adding a new vertex, we add the cost-so-far to its weight

# Code
```cpp
void solve(vector<vector<pair<int, int>>> graph, int n, int m) {
    unordered_map<int, bool> visited;

    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, 1});

    while (!pq.empty()) {
        auto f = pq.top();  // f.first=edge weight ;;; f.second=edge index
        pq.pop();

        if (f.second == n - 1) {
            cout << f.first;
            return;
        }

        visited[f.second] = true;

        for (auto neighbor : graph[f.second]) {
            if (visited[neighbor.second]) {
                continue;
            }

            pq.push({neighbor.first + f.first, neighbor.second});
        }
    }

    cout << -1;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/pepcoder-and-reversing-official/ojquestion
