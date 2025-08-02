# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/140940598-a19411f4-0876-44d4-8a5d-a474078e9a01.png)

[Tutorial](https://www.youtube.com/watch?v=yc0LunmJA1A&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=14)

# Thought Process

- DP cell represents amount to be paid
- For each coin, check every amount
- If `amount - coin` can be achieved in `x` ways, then `amount` can be achieved in `x + 1` ways

![image](https://user-images.githubusercontent.com/10897423/140940368-b51cf15a-fbfe-4849-bbfe-14e951af66ac.png)

- Since this is for combinations, each coin is checked only once for every amount, and therefore the coins' loop is outside the amounts' loop. For permutations, each coin is check for all amount cells, so coin loop would be inside

# Code
```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        int n = size(coins);
        vector<int> dp(amount + 1, 0);
        dp[0] = 1;

        for(auto c: coins) {
            for(int i = c; i <= amount; ++i) {
                dp[i] += dp[i - c];
            }
        }

        return dp[amount];
    }
};
```

# Problem Links
- https://leetcode.com/problems/coin-change-2/
