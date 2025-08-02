# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=xlgZ10436ks&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=79)

# Thought Process
- both the player have two options either they can choose the first element
- or they can choose the last element
- they will choose that particular element which will give them the maximum profit
- as player A wants to maximize its profit
- and player B wants to minimize the difference between them
- hence both will choose the maximum value only

- Choose either first or last element, and subtract optimal result of remaining subarray from its score

# Code
```cpp
class Solution {
    vector<int> stones;
    int dp[1001][1001];

    int helper(int i, int j, int sum) {
        if(i == j || sum <= 0) return 0;

        if(dp[i][j] != -1) return dp[i][j];

        return dp[i][j] = max(
            sum - stones[i] - helper(i + 1, j, sum - stones[i]),
            sum - stones[j] - helper(i, j - 1, sum - stones[j])
        );
    }
public:
    int stoneGameVII(vector<int>& stones) {
        this->stones = stones;
        memset(this->dp, -1, sizeof this->dp);
        int sum = 0;
        for(auto s: stones) sum += s;
        return helper(0, stones.size() - 1, sum);
    }
};
```

# Problem Links
- https://leetcode.com/problems/stone-game-vii/
