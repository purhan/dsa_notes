# Problem Statement

An ugly number is a positive integer whose prime factors are limited to 2, 3, and 5.

Given an integer n, return the nth ugly number.

[Tutorial](https://www.youtube.com/watch?v=Lj68VJ1wu84&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=65)

# Thought Process
- n'tg ugly number depends on the powers of 2, 3, and 5
- On each iteration, check for next power of 2, 3, and 5. Whichever is the smallest is the i'th ugly number, increment that power and move to next iteration

# Code
```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> dp(n + 1);
        dp[1] = 1;

        int p2 = 1, p3 = 1, p5 = 1;

        for(int i = 2; i <= n; ++i) {
            int f2 = dp[p2] * 2;
            int f3 = dp[p3] * 3;
            int f5 = dp[p5] * 5;

            dp[i] = min({f2, f3, f5});

            if(dp[i] == f2) p2++;
            if(dp[i] == f3) p3++;
            if(dp[i] == f5) p5++;
        }

        return dp[n];
    }
};
```

# Problem Links
- https://leetcode.com/problems/ugly-number-ii/
