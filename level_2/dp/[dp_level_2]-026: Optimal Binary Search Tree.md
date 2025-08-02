# Problem Statement
1. You are given two arrays -
The first array(keys), which is sorted and has distinct integers, represents search keys.
Second one(freq) represents frequency counts, where freq[i] is the number of searches to keys[i].
2. A binary search tree is constructed containing all keys and the total cost of searches is minimum.
3. The cost of a BST node is the level of that node multiplied by its frequency.
4. You have to find the minimum cost of all searches.

[Tutorial](https://www.youtube.com/watch?v=HnslzEs8dbY&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=27)

# Thought Process
- Watch tutorial from 54:40 for quick revision, or full tutorial for better idea

# Code
```cpp
void solve(vector<int> keys, vector<int> freq, int n) {
    vector<vector<int>> dp(n, vector<int>(n, 0));

    for (int g = 0; g < n; ++g) {
        for (int i = 0, j = g; j < n; ++i, ++j) {
            if (g == 0) {
                dp[i][j] = freq[i];
            } else if (g == 1) {
                int f1 = freq[i];
                int f2 = freq[j];
                dp[i][j] = min(f1 + 2 * f2, f2 + 2 * f1);
            } else {
                int mn = INT_MAX - 1;
                int freqsum = 0;                // **********************************
                for (int x = i; x <= j; ++x) {  // optimize this part with prefix sum
                    freqsum += freq[x];         // **********************************
                }

                for (int k = i; k <= j; ++k) {
                    int left = (k == i ? 0 : dp[i][k - 1]);
                    int right = (k == j ? 0 : dp[k + 1][j]);

                    mn = min(mn, left + right + freqsum);
                }
                dp[i][j] = mn;
            }
        }
    }

    cout << dp[0][n - 1];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/optimal-bst-official/ojquestion
