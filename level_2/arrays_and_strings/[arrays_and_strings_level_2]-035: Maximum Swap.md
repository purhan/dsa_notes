# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138445910-ab52d78f-530c-48b3-85b2-0bd44a0b9d7e.png)

[Tutorial](https://www.youtube.com/watch?v=IiAd7twX0xU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=35)

# Thought Process
- Theoretically, we want to traverse from left to right, and for each index, we want to check if a bigger digit exists towards its right. And we will swap the first such index.
- Also, for the "bigger digit" on the right, we should swap with its **last** occurence in the number to get the biggest possible number

# Code

Cleaner Code:

```cpp
class Solution {
public:
    int maximumSwap(int num) {
        string s = to_string(num);
        map<int, int> lastOccurenceOfDigit;

        for(int i = 0; i < s.length(); ++i) {
            lastOccurenceOfDigit[s[i] - '0'] = i;
        }

        for(int i = 0; i < s.length(); ++i) {
            for(int j = 9; j > s[i] - '0'; --j) {
                if(lastOccurenceOfDigit[j] > i) {
                    swap(s[i], s[lastOccurenceOfDigit[j]]);
                    return stoi(s);
                }
            }
        }

        return num;
    }
};
```

Other ~~nasty~~ one pass implementation without using map:

```cpp
class Solution {
public:
    int maximumSwap(int num) {
        string s = to_string(num);

        int max_so_far = -1, max_num_index = -1, last_swap_index = -1, right_swap_index = -1;
        for(int i = s.length() - 1; i >= 0; --i) {
            if(int(s[i] - '0') > max_so_far) {
                max_so_far = s[i] - '0';
                max_num_index = i;
            } else if(int(s[i] - '0') < max_so_far) {
                last_swap_index = i;
                right_swap_index = max_num_index;
            }
        }

        if(last_swap_index == -1) {
            return num;
        }

        swap(s[last_swap_index], s[right_swap_index]);

        return stoi(s);
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-swap/
