# Problem Statement
1. You are given a string.
2. You have to print the count of distinct and non-empty subsequences of the given string. 
Note - String contains only lowercase letters.

# Thought Process
- Create a 1D DP
- Each cell stores the count of distinct subsequences till a the substring to that character (0 ... ch)
- The flow is like this:
  - With each cell, first all the previous subsequences will be there from the previous cell. Say there are `x` such subsequences
  - We can append our character to all those subsequences and create `x` more subsequences
  - Ideally we should have `2x` subsequences if `x` is the count from previous cell, but some subsequences may be repeating (counted twice)
  - If a character occurs twice in the string, its previous occurrence would be repeated this time, so we just subtract that (look at the code for better understanding)

![image](https://user-images.githubusercontent.com/10897423/133962200-b0433f20-5b1e-48a4-b82a-be7935318358.png)

# Code
```cpp
long long int solve(string str) {
    int n = str.length();
    vector<long long int> dp(n + 1, 0);
    dp[0] = 1;

    map<char, int> lo;

    for (int i = 1; i <= n; ++i) {
        dp[i] = dp[i - 1] * 2;

        char ch = str[i - 1];

        if (lo.find(ch) != lo.end()) {
            int j = lo[ch];
            dp[i] = dp[i] - dp[j - 1];
        }

        lo[ch] = i;
    }
    return dp[n] - 1;
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/count-distinct-subsequences-official/ojquestion