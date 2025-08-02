# Problem Statement
1. Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.
2. An integer a is closer to x than an integer b if:

        |a - x| < |b - x|, or
        |a - x| == |b - x| and a < b

[Tutorial](https://www.youtube.com/watch?v=1otAwCQG7XM&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=6)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134776491-2d88db37-b484-42cb-babb-1562667f42e2.png)

- In a separate array `gap`, store the difference of each element with `x`.
- Write a comparator to sort based on that gap
- No need to sort all elements since we have to find only `k` closest
- Traverse and find index of the minimum gap element
- From that index, launch 2 pointers in both directions and compare till you get `k` closest elements


# Code

```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find_k_closest_elements/ojquestion#!
- https://leetcode.com/problems/find-k-closest-elements/
