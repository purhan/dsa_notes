# Problem Statement
A topological sort is an ordering of the nodes of a directed graph such that if
there is a path from node a to node b, then node a appears before node b in the
ordering.

[Tutorial](https://www.youtube.com/watch?v=6Vi5Td_a8B8&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=18)

[Article in USACO guide](https://usaco.guide/CPH.pdf#page=159)

# Thought Process

> This implementation uses DFS. Check YT tutorial for BFS

# Code
```cpp
#include <bits/stdc++.h>
using namespace std;

#define pb push_back

int N; // Number of nodes
vector<int> graph[100000], top_sort; // Assume that this graph is a DAG
bool visited[100000];

void dfs(int node) {
	for (int i : graph[node]) {
		if (!visited[i]) {
			visited[i] = true;
			dfs(i);
		}
	}
	top_sort.pb(node);
}

void compute() {
	for (int i = 0; i < N; i++) {
		if (!visited[i]) {
			visited[i] = true;
			dfs(i);
		}
	}
	reverse(begin(top_sort),end(top_sort));
	// The vector `top_sort` is now topologically sorted
}

int main() {
	int M; cin >> N >> M;
	for (int i = 0; i < M; ++i) {
		int a, b; cin >> a >> b;
		graph[a - 1].pb(b - 1);
	}
	compute();
	vector<int> ind(N);
	for (int i = 0; i < N; i++) ind[top_sort[i]] = i;
	for (int i = 0; i < N; i++) for (int j: graph[i]) if (ind[j] <= ind[i]) {
		cout << "IMPOSSIBLE\n"; // topological sort wasn't valid
		exit(0);
	}
	for (int i : top_sort) cout << i + 1 << " ";
	cout << "\n";
}
```

# Problem Links
