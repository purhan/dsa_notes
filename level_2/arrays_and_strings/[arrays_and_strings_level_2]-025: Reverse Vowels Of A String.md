# Problem Statement
Given a string s, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both cases.

Example:

Input: s = "hello"
Output: "holle"

[Tutorial](https://www.youtube.com/watch?v=hgtH9FIZrOE&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=25)

# Thought Process
- Use 2 pointers to swap vowels at each pointer

# Code
```cpp
class Solution {
public:
    string reverseVowels(string s) {
        unordered_map<char, bool> isVowel = {{'a', 1}, {'e', 1}, {'i', 1}, {'o', 1}, {'u', 1}, {'A', 1}, {'E', 1}, {'I', 1}, {'O', 1}, {'U', 1}};

        int n = s.length();
        int l = 0, r = n - 1;

        while(l < r) {
            if(isVowel[s[l]] && isVowel[s[r]]) {
                swap(s[l], s[r]);
                l++;
                r--;
            } else if(isVowel[s[l]]) {
                r--;
            } else if(isVowel[s[r]]) {
                l++;
            } else {
                l++;
                r--;
            }
        }

        return s;
    }
};
```

# Problem Links
- https://leetcode.com/problems/reverse-vowels-of-a-string/
