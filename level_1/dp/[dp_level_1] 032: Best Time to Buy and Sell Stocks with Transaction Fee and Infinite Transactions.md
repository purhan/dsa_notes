# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/142216115-b678f923-521c-4105-a35f-914a47e4ba0b.png)

[Tutorial](https://www.youtube.com/watch?v=pTQB9wbIpfU&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=32)

# Thought Process
- 2 states on each day. Either, we have a remaining stock that can be sold (bought state profit), or we have no stocks right now and we can BUY one now (sold state profit)

# Code
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = size(prices);
        int obsp = -prices[0];
        int ossp = 0;

        for(int i = 1; i < n; ++i) {
            int nbsp = max(obsp, ossp - prices[i]);
            int nssp = max(ossp, obsp + prices[i] - fee);

            obsp = nbsp;
            ossp = nssp;
        }

        return ossp;
    }
};
```

# Problem Links
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/
