# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139535862-49c05c45-34e6-43da-b862-943da4d28686.png)

[Tutorial](https://www.youtube.com/watch?v=3GsK-H_dI9o&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=64)

# Thought Process
- Think of all cases
- If sum of all digits is already divisible by 3, we dont need to do anything (other than converting ans "00000" to "0")
- If sum gives remainder 2, then 2 things are possible:
    - Some digit gives remainder 2, just remove the smallest such digit (array would be sorted so no worries finding the smallest)
    - Some 2 digits each give remainder 1, if above is not true, then this is our only option
    - If both are not found, answer would remain empty ""
- If sum gives remainder 1, then 2 things are possible:
    - Some digit gives remainder 1, just remove the smallest such digit (array would be sorted so no worries finding the smallest)
    - Some 2 digits each give remainder 2, if above is not true, then this is our only option
    - If both are not found, answer would remain empty ""

# Code
```cpp
class Solution {
public:
    string largestMultipleOfThree(vector<int>& digits) {
        int sum = 0, n = size(digits);

        for(int i = 0; i < n; ++i) {
            sum += digits[i];
        }
        sort(digits.begin(), digits.end());

        if(sum % 3 == 2) {
            bool singlePossible = false;

            for(int i = 0; i < n; ++i) {
                if(digits[i] % 3 == 2) {
                    singlePossible = true;
                    digits[i] = -1;
                    break;
                }
            }

            if(!singlePossible) {
                int n1 = -1, n2 = -1;
                for(int i = 0; i < n; ++i) {
                    if(digits[i] % 3 == 1) {
                        if(n1 == -1) {
                            n1 = digits[i];
                            digits[i] = -1;
                        } else {
                            n2 = digits[i];
                            digits[i] = -1;
                            break;
                        }
                    }
                }
            }
        } else if(sum % 3 == 1) {
            bool singlePossible = false;

            for(int i = 0; i < n; ++i) {
                if(digits[i] % 3 == 1) {
                    singlePossible = true;
                    digits[i] = -1;
                    break;
                }
            }

            if(!singlePossible) {
                int n1 = -1, n2 = -1;
                for(int i = 0; i < n; ++i) {
                    if(digits[i] % 3 == 2) {
                        if(n1 == -1) {
                            n1 = digits[i];
                            digits[i] = -1;
                        } else {
                            n2 = digits[i];
                            digits[i] = -1;
                            break;
                        }
                    }
                }
            }
        }

        string ans = "";
        for(int i = n - 1; i >= 0; --i) {
            if(digits[i] != -1) ans += to_string(digits[i]);
        }
        if(ans[0] == '0') ans = "0";
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/largest-multiple-of-three/
