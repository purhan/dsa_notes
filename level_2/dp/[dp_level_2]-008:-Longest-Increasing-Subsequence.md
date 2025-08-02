# Problem Statement
1. You are given a number n, representing the number of elements.
2. You are given n numbers, representing the contents of array of length n.
3. You are required to print the length of longest increasing subsequence of array.

[Tutorial](https://www.youtube.com/watch?v=odrfUCS9sQk&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=1)

# Thought Process

- Create a 1-D DP

![image](https://user-images.githubusercontent.com/10897423/133918792-ee7d9842-a71f-4e57-9dad-7b92e0d92d1f.png)

- Each cell stores the **Longest Increasing Subsequence ending at that element**
- In the screenshot, we are storing the longest increasing subsequence ending at 41. So we check:
  - All cells that are smaller than 41
  - Only on those subsequences, 41 can be appended
  - 41 cannot be added behind 50 for example
  - we take the maximum of all such subsequences

# Code
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = size(nums), ans = 1;
        vector<int> dp(n + 1, 0);
        dp[0] = 1;
        
        for(int i = 1; i < n; ++i) {
            
            for(int j = 0; j < i; j++) {
                if(nums[j] < nums[i]) {
                    dp[i] = max(dp[i], dp[j]);
                }
            }
            dp[i]++;
            ans = max(ans, dp[i]);
        }

        return ans;
    }
};
```