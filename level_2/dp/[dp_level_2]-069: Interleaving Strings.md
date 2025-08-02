# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/145017975-72d8aff1-a392-4960-9b12-a676e5354598.png)

[Tutorial](https://www.youtube.com/watch?v=79g3LJoQk_U&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=71)

# Thought Process
- Tutorial showed iterative, I only did recursive
- Include exclude principle. Choose 2 pointers on s1 and s2. If characters on both pointers are equal to the one on s3, we can choose either, else if only one matches, we can choose that one. If none of the two match, instantly return false

# Code
```cpp
class Solution {
    string s1, s2, s3;
    vector<vector<int>> dp = vector<vector<int>>(105, vector<int>(105, -1));

    bool helper(int i, int j) {
        int k = i + j;

        if(i > s1.length() || j > s2.length() || k > s3.length()) return false;

        if(k == s3.length()) {
            if(i == s1.length() && j == s2.length()) return true;
            else return false;
        }

        if(dp[i][j] != -1) return dp[i][j];

        if(s3[k] == s2[j] && s3[k] == s1[i]) {
            bool choose1 = helper(i + 1, j);
            bool choose2 = helper(i, j + 1);
            return dp[i][j] = choose1 || choose2;
        } else if(s3[k] == s2[j]) {
            return dp[i][j] = helper(i, j + 1);
        } else if(s3[k] == s1[i]) {
            return dp[i][j] = helper(i + 1, j);
        } else {
            return dp[i][j] = false;
        }
    }
public:
    bool isInterleave(string s1, string s2, string s3) {
        this->s1 = s1;
        this->s2 = s2;
        this->s3 = s3;
        return helper(0, 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/interleaving-string/
