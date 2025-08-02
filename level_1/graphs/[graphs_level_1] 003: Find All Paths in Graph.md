# Problem Statement
Given a directed acyclic graph (DAG) of n nodes labeled from 0 to n - 1, find all possible paths from node 0 to node n - 1 and return them in any order.

[Tutorial](https://www.youtube.com/watch?v=DrQ-eTN2v3A&list=PL-Jc9J83PIiHfqDcLZMcO9SsUDY4S3a-v&index=4)  
[LC Article](https://leetcode.com/problems/all-paths-from-source-to-target/discuss/752625/C%2B%2B-DFS-based-Simple-Solution-Explained-100-Time-~80-Space)

# Thought Process

- Create a `res` vector
- Create a `psf` vector
- DFS over a node, add all the visited node to `psf` everytime
- When reached target, add `psf` to `res`
- Remove that node from `psf`, we are backtracking by doing this

# Code
```cpp
class Solution {
public:
    int target;
    vector<int> psf;
    vector<vector<int>> result;

    void dfs(vector<vector<int>>& graph, int currNode) {
        psf.push_back(currNode);

        if(currNode == target) {
            result.push_back(psf);
        } else {
            for(auto node : graph[currNode]) {
                dfs(graph, node);
            }
        }

        psf.pop_back();
    }

    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        target = size(graph) - 1;
        dfs(graph, 0);
        return result;
    }
};
```

# Problem Links
https://leetcode.com/problems/all-paths-from-source-to-target/
