# Problem Statement
There is a forest with an unknown number of rabbits. We asked n rabbits "How many rabbits have the same color as you?" and collected the answers in an integer array answers where answers[i] is the answer of the ith rabbit.

Given the array answers, return the *minimum* number of rabbits that could be in the forest.

[Tutorial](https://www.youtube.com/watch?v=9mEUIdP4ytw&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=38)

# Thought Process
- If a rabbit says there are `x` rabbits with same color, that means atleast `x + 1` rabbits have the same color
- If all `x + 1` rabbits give answer `x`, we have no problem saying that they belong to the same color
- If more than `x + 1` rabbits give the answer `x`, it means that there exists another color for which there are total `x + 1` rabbits

- So, if `y` rabbits give the answer `x`, that means that for every `x + 1` rabbits of those `y` rabbits, we have to create a new color
- So, those `y` rabbits will give in total, `ceil(y / x + 1) * (x + 1)`
- For example:
  - Rabbit says 2 (3 rabbits have that color, 1 found)
  - Rabbit says 2 (3 rabbits have that color, 2 found)
  - Rabbit says 2 (3 rabbits have that color, 3 found)
  - Rabbit says 2 (3 rabbits have that color, 4 found) --> (3 rabbits had color red, all 3 found | 3 rabbits have blue color, 1 found)

# Code
```cpp
class Solution {
public:
    int numRabbits(vector<int>& answers) {
        int ans = 0;
        map<int, int> mp;

        for(auto i: answers)
            mp[i + 1]++;

        for(auto [i, j]: mp)
            ans += i * ceil(j * 1.0 / i);

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/rabbits-in-forest/
