# Problem Statement
1. Given an array of integers nums, calculate the pivot index of this array.
2. The pivot index is the index where the sum of all the numbers strictly to the left of the index is equal to the sum of all the numbers strictly to the index's right.
3. If the index is on the left edge of the array, then the left sum is 0 because there are no elements to the left. This also applies to the right edge of the array.
4. Return the leftmost pivot index. If no such index exists, return -1.

[Tutorial](https://www.youtube.com/watch?v=AH-YhFNJoas&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=5)

# Thought Process

> **DO NOT:** Do not find suffix sum. Do this problem with prefix sum only. Use the sum of whole array instead of suffix sum.

- Precalculate prefix sum (sum of all elements till that cell) and store that in an array
- Find sum of whole array
- Traverse, and for every cell, compare `prefixSum` with `totalSum - prefixSum`

# Code
```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find_pivot_index/ojquestion
