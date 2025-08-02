# Problem Statement
Given a string s, return true if the s can be palindrome after deleting at most one character from it.

[Tutorial](https://www.youtube.com/watch?v=nMjhRtYg2_A&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=32)

# Thought Process

# Code
```cpp
class Solution {
    bool isPalindrome(string s, int i, int j) {
        while(i < j) {
            if(s[i] != s[j]) return false;
            i++;
            j--;
        }
        return true;
    }
public:
    bool validPalindrome(string s) {
        int i = 0, j = s.length() - 1;
        while(i < j) {
            if(s[i] == s[j]) {
                i++;
                j--;
            } else {
                return isPalindrome(s, i + 1, j) || isPalindrome(s, i, j - 1);
            }
        }

        return true;
    }
};
```

# Problem Links
- https://leetcode.com/problems/valid-palindrome-ii