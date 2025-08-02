# Problem Statement
**Minimum Spanning Trees**: A subset of the edges of a connected, undirected, edge-weighted graph that connects all the vertices to each other of minimum total weight, where no cycles are allowed.
In other words, a tree generated from a graph with maximum possible weight for any possible tree.

[Tutorial](https://www.youtube.com/watch?v=Vw-sktU1zmc&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=16)

[Strivers tutorial](https://www.youtube.com/watch?v=HnD676J56ak)

[Article in USACO guide](https://usaco.guide/CPH.pdf#page=157)

# Thought Process

This comes from striver's tutorial:
- Pick a node and add it to our MST
- Take the minimum edge connected to that node, and add that second node to our MST
- Again, for all nodes, take the smallest weight edge, and connect that node to our MST
- Stop when all the nodes have been connected

![image](https://user-images.githubusercontent.com/10897423/138690742-0557dc0e-58b9-47dd-9fc0-ac0e5ddb0842.png)

![image](https://user-images.githubusercontent.com/10897423/138690783-bb46624c-1d85-4142-96ba-bbd5a2a2e879.png)

![image](https://user-images.githubusercontent.com/10897423/138690809-fa38573d-9d70-4069-bcf3-585cc60236d7.png)

![image](https://user-images.githubusercontent.com/10897423/138690845-5b9d4085-435a-4e1c-aaac-311981577123.png)


> This implementation uses DFS. Check YT tutorial for BFS

# Code
```cpp
#include <iostream>
#include <vector>
#include <set>
using namespace std;

typedef long long ll;
typedef pair<int, ll> pl;
typedef vector<int> vi;

#define pb push_back
#define mp make_pair


vector<pl> adj[200000];
int n;

ll prim(){
	ll weight = 0;
	vector<ll> minn(n, INT_MAX);
	minn[0] = 0;
	set<pl> s;
	s.insert({0, 0});
	vector<bool> visited(n, false);

	for (int i = 0; i < n; ++i) {
		if (s.empty()) return -1;

		int v = s.begin() -> first;
		visited[v] = true;
		weight += s.begin() -> second;
		s.erase(s.begin());

		for (auto e : adj[v]) {
			if(!visited[e.first] && e.second < minn[e.first]) {
				s.erase({minn[e.first], e.first});
				minn[e.first] = e.second;
				s.insert({e.second, e.first});
			}
		}
	}
	return weight;
}
int main() {
	int m; cin >> n >> m;
	for (int i = 0; i < m; i++){
		int a, b; ll c;
		cin >> a >> b >> c;
		a--; b--;
		adj[a].pb(mp(b, c));
		adj[b].pb(mp(a, c));
	}
	ll ans = prim();
	if(ans == -1){
		cout << "IMPOSSIBLE";
	}
	else{
		cout << ans;
	}
	return 0;
}
```

# Problem Links
