# Problem Statement
1. You are given a boolean expression with symbols T,F, and operators &,|,^ , where:
```
    T represents True
    F represents False
    & represents boolean AND
    | represents boolean OR
    ^ represents boolean XOR.
```
3. You have to find the number of ways in which the expression can be parenthesized so that the value of expression evaluates to true.

[Tutorial](https://www.youtube.com/watch?v=JbRsM2X2_pg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=25)

# Thought Process

> Explanation needs improvement

- Based on MCM, but quite difficult!
- Take **two** 2D DP tables
- One stores True states, other stores False states

![image](https://user-images.githubusercontent.com/10897423/134815475-6a7fcd96-d132-4589-b220-fcd343a21bf6.png)

- Remember the recurrence relation from the screenshot and think how its achieved

# Code
```cpp
void solve(string str1, string str2) {
    int n = str1.length();

    vector<vector<int>> dpt(n, vector<int>(n, 0));
    vector<vector<int>> dpf(n, vector<int>(n, 0));

    for (int g = 0; g < n; ++g) {
        for (int i = 0, j = g; j < n; ++i, ++j) {
            if (g == 0) {
                dpt[i][j] = (str1[i] == 'T');
                dpf[i][j] = (str1[i] != 'T');
            } else {
                for (int k = i; k < j; ++k) {
                    char oprtr = str2[k];
                    int ltc = dpt[i][k];
                    int rtc = dpt[k + 1][j];

                    int lfc = dpf[i][k];
                    int rfc = dpf[k + 1][j];

                    if (oprtr == '&') {
                        dpt[i][j] += ltc * rtc;
                        dpf[i][j] += lfc * rtc + ltc * rfc + lfc * rfc;
                    } else if (oprtr == '|') {
                        dpt[i][j] += ltc * rtc + lfc * rtc + ltc * rfc;
                        dpf[i][j] += lfc * rfc;
                    } else if (oprtr == '^') {
                        dpt[i][j] += ltc * rfc + lfc * rtc;
                        dpf[i][j] += lfc * rfc + ltc * rtc;
                    }
                }
            }
        }
    }

    cout << dpt[0][n - 1];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/boolean-parenthesization-official/ojquestion
