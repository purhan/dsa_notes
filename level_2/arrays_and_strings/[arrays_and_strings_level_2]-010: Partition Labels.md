# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138222237-9c414424-f48b-4173-88cf-825990c93959.png)

[Tutorial](https://www.youtube.com/watch?v=_I9di3CUOx4&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=11)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/138221759-ba932411-c14b-419c-9abb-b334988fa80e.png)

- Create a map that stores last occurence of a character
- Till that lastIndex, check if all characters within that index also have their last occurence within that index
- If lastIndex of a character exceeds our current lastIndex, simply extend lastIndex

# Code
```cpp
class Solution {
public:
    vector<int> partitionLabels(string s) {
        int n = s.length();

        // store last index of each char
        map<char, int> lastIdx;
        for(int i = 0; i < n; ++i) {
            lastIdx[s[i]] = i;
        }

        vector<int> ans;
        int curMax = 0, cnt = 0;

        // check at each index if all characters before that index have their lastIdx before that index
        for(int i = 0; i < n; ++i) {
            curMax = max(curMax, lastIdx[s[i]]);
            cnt++;
            if(i == curMax) {
                ans.push_back(cnt);
                cnt = 0;
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/partition-labels/
