# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144067825-eccc1085-64cd-415e-b737-4e0c7d5e60ec.png)

[Tutorial](https://www.youtube.com/watch?v=B7UvKpZtgHw&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=27)

# Thought Process
- First, sort by the basis of edge type to process the common edges (type 3) first
- Process each edge one by one
- If an edge already doesn't exist, join the two vertices (on both DSUs for type 3, or on one of the 2 for each type). Increment `count` while doing so. Skip over edges that already exist.
- In the end, if all nodes are joined on both DSUs (which we keep track of using connectedA and connectedB) the return the count of edges that were not used (got skipped)

# Code
```cpp
class DSU {
private:
    vector<int> parent, size;
public:
    DSU(int n)
    {
        parent = vector<int>(n);
        size = vector<int>(n, 1);
        iota(begin(parent), end(parent), 0);
    }

    int getParent(int x)
    {
        if (parent[x] == x) return x;
        return parent[x] = getParent(parent[x]);
    }

    void join(int x, int y)
    {
        x = getParent(x);
        y = getParent(y);
        if (size[x] > size[y])
            swap(x, y);
        if (x == y) return;
        parent[x] = y;
        size[y] += size[x];
    }

    int getSize(int x)
    {
        return size[x] = size[getParent(x)];
    }
};

class Solution {
public:
    int maxNumEdgesToRemove(int n, vector<vector<int>>& edges) {
        int ans = 0;
        sort(edges.begin(), edges.end(), [] (vector<int> &a, vector<int> &b) { return a[0] > b[0]; });

        int connectedA = 1, connectedB = 1;
        int usedEdges = 0;
        DSU alice(n + 1), bob(n + 1);

        for(auto e: edges) {
            int x = e[1], y = e[2];

            if(e[0] == 3) {
                if(alice.getParent(x) != alice.getParent(y)) {
                    alice.join(x, y);
                    bob.join(x, y);
                    usedEdges++;
                    connectedA++;
                    connectedB++;
                }
            } else if(e[0] == 2) {
                if(bob.getParent(x) != bob.getParent(y)) {
                    bob.join(x, y);
                    usedEdges++;
                    connectedB++;
                }
            } else {
                if(alice.getParent(x) != alice.getParent(y)) {
                    alice.join(x, y);
                    usedEdges++;
                    connectedA++;
                }
            }
        }
        if(connectedA != n || connectedB != n) return -1;
        return edges.size() - usedEdges;
    }
};
```

# Problem Links
- https://leetcode.com/problems/remove-max-number-of-edges-to-keep-graph-fully-traversable/
