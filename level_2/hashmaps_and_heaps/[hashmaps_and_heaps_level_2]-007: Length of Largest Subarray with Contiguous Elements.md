# Problem Statement
1. You are given an array(arr) of integers. Values may be duplicated.
2. You have to find the length of the largest subarray with contiguous elements.

[Tutorial](https://www.youtube.com/watch?v=37MdIo-MaSU&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=7)

# Thought Process
- Approach is O(n^2)
- For every element `i`, we run another for loop
- For every `i` and `j` (or for every subarray), we check the following condition

![image](https://user-images.githubusercontent.com/10897423/136176263-5e536b1b-1a06-41d8-9f7d-da3abc8c129d.png)

- We simply print the max of all such occurences

# Code

![image](https://user-images.githubusercontent.com/10897423/136176454-6c80529c-9731-4368-8669-ede03b9b1bb3.png)

```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/largest-subarray-with-contiguous-elements-official/ojquestion
