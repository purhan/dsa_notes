# Problem Statement
1. You are given an array(arr) of integers.
2. You have to find the length of the largest subarray with sum 0.

[Tutorial](https://www.youtube.com/watch?v=_yGf2rxwZlA&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=5)

# Thought Process
- Traverse from left to right, compute the prefix sum and store it in an array
- If you ever encounter the same sum again, that means that from its last occurence to this occurence, the sum is zero

![image](https://user-images.githubusercontent.com/10897423/136063185-f926cbd5-8d86-4fc7-8ee3-40a8307c2262.png)

- In the screenshot, `2` occured twice, so that subarray has sum zero

# Code

![image](https://user-images.githubusercontent.com/10897423/136063345-1d454034-a73f-4a85-a903-76db2d2d5ad8.png)

```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/largest-subarray-with-zero-sum-official/ojquestion
