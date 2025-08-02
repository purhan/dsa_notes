# Problem Statement
1. Write an efficient algorithm that searches for a target value in an m x n integer matrix. The matrix has the following properties:
a). Integers in each row are sorted in ascending from left to right.
b). Integers in each column are sorted in ascending from top to bottom.

[Tutorial](https://www.youtube.com/watch?v=iZ4xURJa0oQ&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=4)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134773919-86fc0465-e73a-4f3a-a30d-8cee039774c0.png)

- Idea is to binary search with respect to the diagonal
- Top right cell is `Biggest in its row and smallest in its column`
  - If that cell is bigger than our target, we discard that column instantly, and check the element to the left
  - If that cell is smaller than our target, we discard that row instandly, and check the element downwards

# Code
```cpp
```
![image](https://user-images.githubusercontent.com/10897423/134774065-aa4894ce-4297-47cc-8c81-c2e8fed47ec9.png)


# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/search_a_2d_matrix_ii/ojquestion
- https://leetcode.com/problems/search-a-2d-matrix-ii/