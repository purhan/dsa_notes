# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/142219963-a85889d0-208e-467a-9099-42ada43cca87.png)

[Tutorial](https://www.youtube.com/watch?v=GY0O57llkKQ&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=33)

# Thought Process

# Code
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty())  return 0;
        int n = prices.size();

        vector<int> buy(n+1), sell(n+1);
        buy[1] = -prices[0], sell[1] = 0;

        for(int i = 2; i <= n; i++) {
            buy[i] = max(buy[i-1], sell[i-2] - prices[i-1]);
            sell[i] = max(sell[i-1], buy[i-1] + prices[i-1]);
        }
        return sell[n];
    }
};
```

# Problem Links
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/