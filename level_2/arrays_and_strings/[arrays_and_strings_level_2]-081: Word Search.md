# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/140064922-286da7b7-3192-41ff-af36-10dac28fc582.png)

[Tutorial](https://www.youtube.com/watch?v=_RKupaYOrzI&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=81)

# Thought Process
- DFS backtracking kinda question
- For each call, mark that cell as visited (by using a foreign character such as '!')

# Code
```cpp
class Solution {
    bool helper(vector<vector<char>>& board, string& word, int& n, int& m, int r, int c, int x) {
        if(x == word.size()) return true;
        if(r < 0 || c < 0 || r >= n || c >= m) return false;
        if(board[r][c] == '!') return false;
        if(board[r][c] != word[x]) return false;

        char ch = board[r][c];
        board[r][c] = '!';

        bool ans = false;
        ans = ans || helper(board, word, n, m, r + 1, c, x + 1);
        ans = ans || helper(board, word, n, m, r - 1, c, x + 1);
        ans = ans || helper(board, word, n, m, r, c + 1, x + 1);
        ans = ans || helper(board, word, n, m, r, c - 1, x + 1);

        board[r][c] = ch;

        return ans;
    }
public:
    bool exist(vector<vector<char>>& board, string word) {
        int n = board.size(), m = board[0].size();

        for(int i = 0; i < board.size(); ++i) {
            for(int j = 0; j < board[0].size(); ++j) {
                if (board[i][j] == word[0] && helper(board, word, n, m, i, j, 0)) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

# Problem Links
- https://leetcode.com/problems/word-search/
