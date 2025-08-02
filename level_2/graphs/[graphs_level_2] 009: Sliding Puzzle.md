# Problem Statement
On an 2 x 3 board, there are five tiles labeled from 1 to 5, and an empty square represented by 0. A move consists of choosing 0 and a 4-directionally adjacent number and swapping it.

The state of the board is solved if and only if the board is [[1,2,3],[4,5,0]].

Given the puzzle board board, return the least number of moves required so that the state of the board is solved. If it is impossible for the state of the board to be solved, return -1.

[Tutorial](https://www.youtube.com/watch?v=-7zxQzs3D2A&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=9)

# Thought Process
- First, since board size is constant for all testcases, we will treat it as a string instead. Our target string is "123450"
- Change the given vector board into a string as shown in code
- Run a BFS and count levels

In the BFS:
- We use a `swapper` to determine what the next string will look like after we traverse in the BFS
- Whatever is the position of `0` in the current string, we will swap that position with all possible positions and add those new formed strings to the BFS queue

# Code
```cpp
class Solution {
public:
    int slidingPuzzle(vector<vector<int>>& board) {
        string target = "123450";

        string init = "";
        for(auto i: board) for(auto j: i) init += '0' + j;

        vector<vector<int>> swapper = {{1, 3}, {0, 2, 4}, {1, 5}, {0, 4}, {1, 3, 5}, {2, 4}};

        unordered_map<string, bool> visited;
        queue<string> q;
        q.push(init);

        int level = 0;
        while(!q.empty()) {
            int level_size = size(q);
            while(level_size--) {
                auto curr_string = q.front();
                q.pop();

                if(visited[curr_string]) continue;
                visited[curr_string] = true;

                if(curr_string == target) return level;

                int i = curr_string.find('0');
                for(auto j: swapper[i]) {
                    string next_string = curr_string;
                    swap(next_string[i], next_string[j]);
                    q.push(next_string);
                }
            }
            level++;
        }
        return -1;
    }
};
```

# Problem Links
- https://leetcode.com/problems/sliding-puzzle/
