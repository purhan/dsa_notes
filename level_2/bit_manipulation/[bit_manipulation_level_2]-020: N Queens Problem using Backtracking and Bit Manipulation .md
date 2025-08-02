# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=7qWsFBBTFRE&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=20)

# Thought Process
- Code pending
- First write the recursive code
- Intuition here is that, to check whether a queen is safe in a cell, we need to check row, column as well as diagonal
- Checking row and col is simple
- To check diagonal, we need to check two diagonals
- In the diagram below, 2nd and 3rd diagrams denote normal diagonal and reverse diagonal
- To cache normal diagonal, we use bitmask to set (row+col)'th bit
- To cache reverse diagonal, we use bitmask to set (row - col + N - 1)'th bit

![image](https://user-images.githubusercontent.com/10897423/148641382-866d4296-effc-4ad9-96c2-ef3255af3e99.png)

# Code
```cpp
```

# Problem Links
