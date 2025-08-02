# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138098140-463d241b-31da-4eda-bb04-4eab3500a0f8.png)

[Tutorial](https://www.youtube.com/watch?v=738Dy3D-q-E&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl)

# Thought Process
- Use two pointers to compare chars in both strings
- If same char, move both pointers
- If different char, compare last char of name with `j`

- In the end, look for two conditions:
- If `name` string is unused (pointer not at the end), then its false, since typed is shorter than original string
- If some `j` is remaining, compare it with last char of `name`

# Code
```cpp
class Solution {
public:
    bool isLongPressedName(string name, string typed) {
        int n = name.length(), m = typed.length();
        int i = 0, j = 0;
        while(i < n && j < m) {
            if(name[i] == typed[j]) {
                i++;
                j++;
            } else if(i > 0 && name[i - 1] == typed[j]) {
                j++;
            } else {
                return false;
            }
        }

        while(j < m) {
            if(name[i - 1] != typed[j]) return false;
            j++;
        }

        if(i != n) return false;

        return true;
    }
};
```

# Problem Links
- https://leetcode.com/problems/long-pressed-name/
