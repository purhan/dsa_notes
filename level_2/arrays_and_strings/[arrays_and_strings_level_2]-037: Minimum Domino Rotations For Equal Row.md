# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138465029-6a6d5372-1168-4153-a75e-28e9d910c73a.png)

[Tutorial](https://www.youtube.com/watch?v=mnYHDE9Kk9s&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=37)

# Thought Process
- Implementation was tricky
- Our only 2 possible candidates for swapping are the first 2 numbers
- If a number doesn't exist neither at top nor at bottom for some position, it's not a possible candidate and we mark it as -1
- If we lose both candidates, return -1

- Check number of occurences for both candidates in both the top and bottom array (so 4 counts) and return the minimum cost count

# Code
```cpp
class Solution {
public:
    int minDominoRotations(vector<int>& tops, vector<int>& bottoms) {
        int n = tops.size();
        int num1 = tops[0], num2 = bottoms[0];
        int cnt1 = 0,   // number of swappings required to make whole array as num1 considering top
        cnt2 = 0,       // number of swappings required to make whole array as num2 considering top
        cnt3 = 0,       // number of swappings required to make whole array as num1 considering bottom
        cnt4 = 0;       // number of swappings required to make whole array as num2 considering bottom

        for(int i = 0; i < n; ++i) {
            if(num1 != tops[i] && num1 != bottoms[i]) num1 = -1;
            if(num2 != tops[i] && num2 != bottoms[i]) num2 = -1;

            if(num1 < 0 && num2 < 0) return -1;

            if(num1 == tops[i]) cnt1++;
            if(num2 == tops[i]) cnt2++;
            if(num1 == bottoms[i]) cnt3++;
            if(num2 == bottoms[i]) cnt4++;
        }

        if(num1 >= 0 && num2 >= 0)
            return min({cnt1, cnt2, cnt3, cnt4, n - cnt1, n - cnt2, n - cnt3, n - cnt4});
        else if(num1 >= 0)
            return min({cnt1, n - cnt1, cnt3, n - cnt3});
        else
            return min({cnt2, n - cnt2, cnt4, n - cnt4});
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-domino-rotations-for-equal-row/
