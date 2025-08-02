# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139240085-c1a4b97e-6849-4d0c-b12c-e36c02823305.png)

[Tutorial](https://www.youtube.com/watch?v=4DQu4Z6f2XI&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=51)
[LC Article](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/discuss/585590/C%2B%2BJava-DFS-and-Math)

# Thought Process

- Learn the idea from tutorial but LC had the better DFS Solution

![image](https://user-images.githubusercontent.com/10897423/139239911-ed45bfa4-11a5-489a-9315-453f28c09995.png)

- DFS over all possible strings, we will be traversing lexographically since this is DFS
- With every new depth, pass last character, and length so far
- If length == n, we have a possible answer. But we want k'th such string, so we will k-- on all such strings and return a string where k == 0
- The string we return will be constructed by backtracking last_characters


# Code
```cpp
class Solution {
    string dfs(int n, int& k, int len, char last_ch) {

        // If string is of length `n`, we want the k'th such string so we decrement k for length n
        if(len == n) {
            k--;
            return "";
        }

        for(char ch = 'a'; ch <= 'c'; ++ch) {
            if(ch != last_ch) {
                auto res = dfs(n, k, len + 1, ch);

                if(k == 0) return ch + res;
            }
        }
        return "";
    }
public:
    string getHappyString(int n, int k) {
        return dfs(n, k, 0, '_');
    }
};
```

# Problem Links
- https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/
