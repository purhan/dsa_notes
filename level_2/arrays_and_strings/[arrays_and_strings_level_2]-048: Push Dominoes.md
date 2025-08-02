# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138817336-20f25244-70ec-462e-bf0e-2907cd32ec7d.png)

[Tutorial](https://www.youtube.com/watch?v=Fo4ORqOLDCY&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=48)

# Thought Process

- Add dummy dominoes on front and end
- Create segments where dominoes are falling, and simulate each segment using 2 pointers

![image](https://user-images.githubusercontent.com/10897423/138817136-ba145b71-8ca9-4476-b521-7e881108a7dd.png)


# Code
```cpp
class Solution {
public:
    string pushDominoes(string dominoes) {
        int n = dominoes.length();
        vector<pair<int, int>> segments;

        dominoes = "L" + dominoes + "R";
        int last_falling = 0;
        for(int i = 1; i < n + 2; ++i) {
            if(dominoes[i] != '.') {
                segments.push_back({last_falling, i});
                last_falling = i;
            }
        }

        for(auto s : segments) {
            int l = s.first, r = s.second;
            if(dominoes[l] != 'R' && dominoes[r] == 'L') {
                while(r >= l) {
                    dominoes[r] = 'L';
                    r--;
                }
            } else if(dominoes[l] == 'R' && dominoes[r] != 'L') {
                while(r >= l) {
                    dominoes[l] = 'R';
                    l++;
                }
            } else if(dominoes[l] == 'R' && dominoes[r] == 'L') {
                while(r > l) {
                    dominoes[l] = 'R';
                    dominoes[r] = 'L';
                    l++;
                    r--;
                }
            }
        }
        dominoes.erase(0, 1);
        dominoes.pop_back();
        return dominoes;
    }
};
```

# Problem Links
- https://leetcode.com/problems/push-dominoes/
