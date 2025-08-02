# Problem Statement
1. You are given a sorted integer array arr containing 1 and prime numbers, where all the integers of arr are unique. You are also given an integer k.

2. For every i and j where 0 <= i < j < arr.length, we consider the fraction arr[i] / arr[j].

3. Return the kth smallest fraction considered. Return your answer as an array of integers of size 2, where answer[0] == arr[i] and answer[1] == arr[j].

[Tutorial](https://www.youtube.com/watch?v=ZwbSRpPOVHg&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=48)

# Thought Process
- Involves binary search on answer
- Binary search answers from `smallest possible ratio (smallest/biggest element) ---to--- 1` range
- Careful, we are dealing with doubles here, so check the binary search code and its conditions carefully

- Binary search over the answer. For each search, the helper function tells us:
  - What is the count of fractions smaller than that query
  - What is the biggest fraction just smaller than that query
  - When we get `cnt == k`, we know that that's the fraction we are asked to return

- Read code to understand how the helper function works

# Code
```cpp
class Solution {
    vector<int> helper(vector<int> arr, double target) {
        int cnt = 0;
        int i = 0;
        int num = arr[0], deno = arr[size(arr) - 1];

        for(int j = 1; j < size(arr); ++j) {
            while(arr[i] <= arr[j] * target) {
                i++;
            }
            cnt += i;
            if(i > 0 && arr[i - 1] * deno > num * arr[j]) {
                num = arr[i - 1];
                deno = arr[j];
            }
        }

        return vector<int>({cnt, num, deno});
    }

public:
    vector<int> kthSmallestPrimeFraction(vector<int>& arr, int k) {
        int n = size(arr);
        vector<int> ans;

        double lo = arr[0] / double(arr[n - 1]), hi = 1;

        while(lo < hi) {
            double mid = (lo + hi) / 2;

            auto cnt = helper(arr, mid); // Trust this function, it returns {count, numerator, denominator}

            if(k < cnt[0]) {
                hi = mid;
            } else if(k > cnt[0]) {
                lo = mid;
            } else {
                ans = {cnt[1], cnt[2]};
                return ans;
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/k-th-smallest-prime-fraction/
