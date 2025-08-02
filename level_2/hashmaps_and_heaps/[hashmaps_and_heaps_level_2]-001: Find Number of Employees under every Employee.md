# Problem Statement
1. You are given number N and 2*N number of strings that contains mapping of the employee and his manager.
2. An employee directly reports to only one manager.
3. All managers are employees but the reverse is not true.
4. An employee reporting to himself is the CEO of the company.
5. You have to find the number of employees under each manager in the hierarchy not just their direct reports.

[Tutorial](https://www.youtube.com/watch?v=bit4Jn-ZoyQ&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR)

# Thought Process
- Simple DFS. Call each child and return its `children + 1`

# Code
```cpp

```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/number-of-employees-under-every-manager-official/ojquestion
