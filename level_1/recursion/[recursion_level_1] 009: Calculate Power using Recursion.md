# Problem Statement
1. You are given a number x.
2. You are given another number n.
3. You are required to calculate x raised to the power n. Don't change the signature of power function.

Note1 -> The previous version expects the call stack to be of n height. This function expects call function to be only log(n) high.

Note2 -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=O84uumjBOMY&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=10)

# Thought Process

# Code
```cpp
class Solution {
public:
    double myPow(double x, int n) {
        if(n == 0) return 1;

        double halfPow = myPow(x, n / 2);

        if(n % 2== 0){
            return halfPow * halfPow;
        }
        else{
            if(n < 0)
                return 1 / x * halfPow * halfPow
            else
                return x * halfPow * halfPow;
        }
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/introduction-to-recursion/power-logarithmic-official/ojquestion
