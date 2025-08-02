# Problem Statement
1. You are given an array of integers(arr) and a number K.
2. You have to find length of the longest subarray whose sum is divisible by K.

[Tutorial](https://www.youtube.com/watch?v=GrV3MTR_Uk0&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=29)

# Thought Process
- Find remainder of sum at each index with the help of prefix sum
- Store the first occurence of the remainder in the map
- Everytime a remainder repeats, that means that from any previous occurence of that remainder to this occurence, the subarray sum would be divisible by k
- From the first occurence to this occurence, the subarray would be the largest, so take the max for all repeating remainders

# Code
```cpp
void solve(vector<int> nums, int n, int k) {
    int pSum = 0, ans = 0;
    map<int, int> firstOccurenceOfRem;

    firstOccurenceOfRem[0] = -1;    // This is for the case when a subarray from index 0->x satisfies the condition
    for (int i = 0; i < n; ++i) {
        pSum += nums[i];

        int rem = pSum % k;
        if (rem < 0) rem += k;

        if (firstOccurenceOfRem.find(rem) == firstOccurenceOfRem.end()) {
            firstOccurenceOfRem[rem] = i;
        }

        ans = max(ans, i - firstOccurenceOfRem[rem]);
    }
    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/longest-subarray-with-sum-divisible-by-k-official/ojquestion#!
