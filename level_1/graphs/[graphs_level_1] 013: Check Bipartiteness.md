# Problem Statement
1. You are given a graph.
2. You are required to find and print if the graph is bipartite

[Tutorial](https://www.youtube.com/watch?v=ZBhZ1DXGrhA&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=13)

> Explained better on USACO guide and Competitive Programmer's Handbook

# Thought Process
- DFS/BFS over the graph
- Try understanding the code below. Check YT tutorial for BFS version

# Code
```cpp
#include <cstdio>
#include <vector>

const int MN = 1e5+10;

int N, M;
bool bad, vis[MN], group[MN];
std::vector<int> a[MN];

void dfs(int n=1, bool g=0)
{
	vis[n]=1;
	group[n]=g;
	for(int u:a[n])
		if(vis[u])
		{
			if(group[u]==g)
				bad=1;
		}
		else
			dfs(u, !g);
}
int main()
{
	scanf("%d%d", &N, &M);
	for(int i=0,u,v;i<M;++i)
		scanf("%d%d", &u, &v), a[u].push_back(v), a[v].push_back(u);
	for(int i=1;!bad && i<=N;++i)
		if(!vis[i])
			dfs(i);
	if(bad)
		printf("IMPOSSIBLE\n");
	else
		for(int i=1;i<=N;++i) printf("%d%c", group[i]+1, " \n"[i==N]);
	return 0;
}
```

# Problem Links
