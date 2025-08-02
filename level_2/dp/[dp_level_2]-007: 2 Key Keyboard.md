# Problem Statement
1. You are given a number N.
2. You have to print exactly N number of 'X' on a notepad by performing the minimum number of operations.
3. Operations allowed are -
   - copyAll -> You can copy all the characters present on the notepad.
   - Paste -> You can paste the last copied characters.
4. You have to find the minimum number of operations to get N 'X'.

Note -> Initially, one 'X' is present on the screen.

[Tutorial](https://www.youtube.com/watch?v=anHoebBokmg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=7)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134677251-21d1580c-eded-473e-b4ca-9c8e6b650df7.png)

- For a number `n`, if we already have `x` characters on screen where `x` is a divisor of `n`, we can `copy-paste` everything `n / x` times
- From this, we come to the conclusion that, we only need to find out the number of Prime Divisors of `n` and that would be the answer. Watch tutorial for clarity.


# Code
```cpp
class Solution {
public:
    int minSteps(int n) {
        int ans = 0;

        for(int i = 2; i * i <= n;) { // Notice the loop carefully, we dont increment `i`
            if((n % i) == 0) {
                ans += i;
                n /= i;
            } else {
                i++;
            }
        }

        if(n != 1) ans += n;

        return ans;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/2-key-keyboard-official/ojquestion
- https://leetcode.com/problems/2-keys-keyboard/
