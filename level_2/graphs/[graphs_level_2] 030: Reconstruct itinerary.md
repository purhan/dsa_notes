# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144254795-dfc31295-3a05-41b6-be4c-1568784e1415.png)

[Tutorial](https://www.youtube.com/watch?v=U33blOQRaJ0&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=30)

# Thought Process
- Standard eularian path question
- Graph should be of type `map<string, minHeap[string]>`
- First, construct the graph (unrelated to solution)

- Run a DFS from main source (JFK in this case)
- While backtracking, add the src to the ans
- In the end, you get eularian path, reverse of which is the ans

- One thing to take care of in DFS -> We can't mark vertices as visited. Instead, we want to mark "paths" as visited, which we are kindof doing by using the priority queue graph approach

# Code
```cpp
typedef unordered_map<string, priority_queue<string, vector<string>, greater<string>>> Graph;

class Solution {
public:
    void dfs(vector<string>& ans, Graph& graph, string src) {
        if(graph[src].empty()) {
            ans.push_back(src);
            return;
        }

        while(!graph[src].empty()) {
            auto t = graph[src].top();
            graph[src].pop();
            dfs(ans, graph, t);
        }
        ans.push_back(src);
    }

    vector<string> findItinerary(vector<vector<string>>& tickets) {
        vector<string> ans;

        // construct graph
        Graph graph;
        for(auto ticket: tickets) {
            graph[ticket[0]].push(ticket[1]);
        }

        dfs(ans, graph, "JFK");
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/reconstruct-itinerary/
