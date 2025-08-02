# Problem Statement
Given an array of integers arr, sort the array by performing a series of pancake flips.

In one pancake flip we do the following steps:

    Choose an integer k where 1 <= k <= arr.length.
    Reverse the sub-array arr[0...k-1] (0-indexed).

For example, if arr = [3,2,1,4] and we performed a pancake flip choosing k = 3, we reverse the sub-array [3,2,1], so arr = [1,2,3,4] after the pancake flip at k = 3.

Return an array of the k-values corresponding to a sequence of pancake flips that sort arr. Any valid answer that sorts the array within 10 * arr.length flips will be judged as correct.

[Tutorial](https://www.youtube.com/watch?v=77YAtclapME&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=46)

# Thought Process
- Simple, just traverse from right to left. Whenever you encounter a cher that's not in the right place, you need to do atleast 1 or atmost 2 operations to bring it in the right place
- Code should be quite self explanatory

# Code
```cpp
```

![image](https://user-images.githubusercontent.com/10897423/136000591-296fcb37-43e4-4a6a-ae7d-d0c948c8c4ae.png)


# Problem Links
- https://leetcode.com/problems/pancake-sorting/
