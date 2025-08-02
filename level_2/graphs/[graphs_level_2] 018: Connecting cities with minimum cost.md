# Problem Statement

There are n cities and there are roads in between some of the cities. Somehow all the roads are damaged simultaneously. We have to repair the roads to connect the cities again. There is a fixed cost to repair a particular road. Find out the minimum cost to connect all the cities by repairing roads.

[Tutorial](https://www.youtube.com/watch?v=k5SVIlN4hio&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=19)

# Thought Process
- Extremely similar to `optimize water distribution` question
- Just implement mst

# Code
```cpp
class Node {
public:

    int nbr, wt;

    Node(int a, int b) {
        this->nbr = a;
        this->wt = b;
    }

    bool operator < (const Node& other) const {
        return wt > other.wt;
    }
};

int n, e;
vector<vector<Node>> graph;

void solve() {
    int ans = 0;
    vector<bool> visited(n + 1, false);

    priority_queue<Node> pq;
    pq.push(Node(0, 0));

    while (!pq.empty()) {
        auto rem = pq.top();
        pq.pop();

        if (visited[rem.nbr]) continue;
        visited[rem.nbr] = true;
        ans += rem.wt;

        for (auto k : graph[rem.nbr]) {
            pq.push(k);
        }
    }

    cout << ans;
}
```

# Problem Links
- https://www.youtube.com/watch?v=k5SVIlN4hio&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=18
