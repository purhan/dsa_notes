# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139424701-1f9e64ed-da2a-405c-b78e-cc230d7abc53.png)

[Tutorial](https://www.youtube.com/watch?v=6cODUSGmYD4&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=58)

# Thought Process
- Thing to notice here is, if k>=2, we can rearrange in any order we want, this is similar to swap sort. So we just return the lexicographically smallest of those (just sort the string)
- Else, we just bruteforce (each time move the first char to last) and return the smallest of all those arrangements

# Code
```cpp
class Solution {
public:
    string orderlyQueue(string s, int k) {
        if(k >= 2) {
            sort(s.begin(), s.end());
            return s;
        }

        string ans = s;
        for(int i = 0; i < s.length(); ++i) {
            s += s[0];
            s.erase(0, 1);
            ans = min(ans, s);
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/orderly-queue/
