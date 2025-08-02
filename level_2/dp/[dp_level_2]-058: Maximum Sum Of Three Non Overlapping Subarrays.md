# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=mXeT7-oZeQQ&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=59)

# Thought Process
- Revise from pepcoding implementation, I sucked at the part where lexicographical comparison was to be done

- Has to do more with prefix, suffix rather than DP
- Calculate prefix sum for all subarrays of size k
- Calculate suffix sum for all subarrays of size k
- Iterate over all indeces, according to current index, you investigate 3 values:
  - sum of current subarray
  - greatest subarray on left, using prefix sum
  - greatest subarray on right, using suffix sum
- Update the answer accordingly

# Code
```cpp
class Solution {
public:
    vector<int> maxSumOfThreeSubarrays(vector<int>& nums, int k) {
        int n = nums.size(); 
        vector<int> psk(n), ps(n);     // prefix sum of last k elements

        for(int i = n - 1; i >= 0; --i) {
            if(i != n - 1) {
                ps[i] = ps[i + 1];
            }
            ps[i] += nums[i];
        }

        // calculate sum of subarrays of length `k` startig at each index
        for(int i = n - k; i >= 0; --i) {
            psk[i] = ps[i];
            if(i < n - k) psk[i] -= ps[i + k];
        }

        vector<int> maxl(n), maxr(n);

        // calculate for each index, the index of the previous subarray with largest sum (store lexicographically smallest)
        for(int i = 0; i < n; ++i) {
            maxl[i] = i;
            if(i > 0) {
                if(psk[maxl[i - 1]] > psk[maxl[i]]) {
                    maxl[i] = maxl[i - 1];
                }
                if(psk[maxl[i - 1]] == psk[maxl[i]]) {
                    if(to_string(maxl[i]) > to_string(maxl[i - 1]))
                    maxl[i] = maxl[i - 1];
                }
            }
        }

        // calculate for each index, the index of the next subrray with largest sum (and store lexicographically smallest)
        for(int i = n - 1; i >= 0; --i) {
            maxr[i] = i;
            if(i < n - 1) {
                if(psk[maxr[i + 1]] > psk[maxr[i]]) {
                    maxr[i] = maxr[i + 1];
                }
            }
        }

        vector<int> ans(3);
        int maxSoFar = -1;

        // for each index, check if 
        // sum of subarray at this index (of length k) 
        // + sum of greatest such subarray on left of it 
        // + sum of greatest such subarray on right of it
        // is the greatest so far. And update the answer lexicographically
        for(int i = k; i <= (n - 2 * k); ++i) {
            int thisSum = psk[i];
            int leftSum = psk[maxl[i - k]];
            int rightSum = psk[maxr[i + k]];
            int total = thisSum + leftSum + rightSum;
            cout << total << endl;
            if(total == maxSoFar) {
                if(to_string(ans[0]) + to_string(ans[1]) + to_string(ans[2]) > to_string(maxl[i - k]) + to_string(i) + to_string(maxr[i + k])) {
                    ans[0] = maxl[i - k];
                    ans[1] = i;
                    ans[2] = maxr[i + k];
                }
            }
            if(total > maxSoFar) {
                maxSoFar = total;
                ans[0] = maxl[i - k];
                ans[1] = i;
                ans[2] = maxr[i + k];
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-sum-of-3-non-overlapping-subarrays/
