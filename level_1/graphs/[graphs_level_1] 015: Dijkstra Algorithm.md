# Problem Statement
Find shortest path in a weighted graph. Doesn't work with Negative weights

[Tutorial](https://www.youtube.com/watch?v=sD0lLYlGCJE&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=15)

[Article in USACO guide](https://usaco.guide/gold/shortest-paths?lang=cpp#implementation-1)

# Thought Process

> This implementation uses DFS. Check YT tutorial for BFS

# Code
```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;
#define pb push_back

vector<pair<int, int>> graph[100000];
// Adjacency list of (neighbour, edge weight)
ll dist[100000];
int N;

void dijkstra(int src) { // Source and destination
	// Set all distances to infinity
	for (int i = 0; i < N; ++i) dist[i] = LLONG_MAX;

	using T = pair<ll,int>; priority_queue<T,vector<T>,greater<T>> pq;
	dist[src] = 0; // The shortest path from a node to itself is 0
	pq.push({0, src});

	while (pq.size()) {
		ll cdist = pq.top().first;
		int node = pq.top().second;
		pq.pop();

		if (cdist != dist[node]) continue;
		for (pair<int, int> i : graph[node]) {
			// If we can reach a neighbouring node faster,
			// we update its minimum distance
			if (cdist+i.second < dist[i.first]) {
				pq.push({dist[i.first] = cdist+i.second, i.first});
			}
		}
	}
}

int main() {
	int M; cin >> N >> M;
	for (int i = 0; i < M; ++i) {
		int a,b,c; cin >> a >> b >> c;
		graph[a-1].pb({b-1,c});
	}
	dijkstra(0);
	for (int i = 0; i < N; ++i) cout << dist[i] << " ";
}
```

# Problem Links
