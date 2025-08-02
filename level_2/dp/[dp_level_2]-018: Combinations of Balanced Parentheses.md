# Problem Statement
1. You are given a number n, representing the number of opening brackets ( and closing brackets )
2. You are required to find the number of ways in which you can arrange the brackets if the closing brackets should never exceed opening brackets

e.g.

for 1, answer is 1 -> ()

for 2, answer is 2 -> ()(), (())

for 3, asnwer is 5 -> ()()(), () (()), (())(), (()()), ((()))

[Tutorial](https://www.youtube.com/watch?v=n-8R95-5MXw&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=18)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134692979-ed83d176-74bd-4367-b375-520640b77c00.png)

- Solution is just Catalan Numbers, think about how to show that to the interviewer
- Carefully observe the combitations for 2 pairs in the screenshot. Use that to derive the equation


# Code
```cpp
void solve(int n) {
    vector<int> dp(n + 1, 0);
    dp[0] = 1;
    dp[1] = 1;

    for (int i = 2; i <= n; ++i) {
        for (int j = 0; j < i; ++j) {
            dp[i] += dp[j] * dp[i - j - 1];
        }
    }

    cout << dp[n];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/count-brackets-official/ojquestion
