# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/142205902-663525c9-9030-48bf-9015-aea1311a91ad.png)

[Tutorial](https://www.youtube.com/watch?v=wuzTpONbd-0&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=35)

# Thought Process
- Read comments in code

# Code
```cpp
// basically similar to buy and sell stock 1

// here at each point, we store best transaction on left (similar to that other question)
// and also store best transaction on right by traversing in reverse
// max sum of both left and right is the answer

class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = size(prices);
        vector<int> dpl(n + 1, 0), dpr(n + 1, 0);

        int minl = prices[0];
        for(int i = 1; i < n; ++i) {
            minl = min(minl, prices[i]);
            dpl[i] = max(dpl[i - 1], prices[i] - minl);
        }

        int maxr = prices[n - 1];
        for(int i = n - 2; i >= 0; --i){
            maxr = max(maxr, prices[i]);
            dpr[i] = max(dpr[i + 1], maxr - prices[i]);
        }

        int ans = 0;
        for(int i = 0; i < n; ++i) ans = max(ans, dpr[i] + dpl[i]);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/
