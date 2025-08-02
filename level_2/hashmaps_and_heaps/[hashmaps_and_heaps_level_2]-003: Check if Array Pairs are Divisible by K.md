# Problem Statement
1. You are given an array(arr) of integers and a number K.
2. You have to find if the given array can be divided into pairs such that the sum of every pair is divisible by k.

[Tutorial](https://www.youtube.com/watch?v=BvKv-118twg&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=3)

# Thought Process
- Simple, to check if there exists a pair whose sum is divisible by k:
  - We need to check the remainder of `a` when divided by k. Call it `remA`
  - We need to check the remainder of `b` when divided by k. Call it `remB`
  - We need to check if `remA + remB` is equal to k

- We store Frequency of all remainders for all numbers in a map
- For each item `a` in array, we check if `k - remA` has the same frequency as `remA`
- Exception cases: remainder = 0 or remainder = k / 2

# Code
```cpp
```
![image](https://user-images.githubusercontent.com/10897423/136057932-119743c1-23d0-4d16-a70e-98aef377c050.png)

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/check-if-an-array-cab-be-divided-into-pairs-whose-sum-is-divisible-by-k-official/ojquestion
