# Problem Statement
1. You are given number N and 2*N number of strings that represent a list of N tickets(source and destination).
2. You have to find the itinerary in order using the given list of tickets.

Assumption - The input list of tickets is not cyclic and there is one ticket from every city except the final destination.

[Tutorial](https://www.youtube.com/watch?v=4mi2rO4D_Xk&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=2)

# Thought Process
- All destinations are represented as a graph
- Two steps:
  - Find root node
  - Do a DFS/BFS (either will work) to print the cities in order

Finding the root node:
- Construct a `hashmap<city, bool>`
- Each time you will get `src -> destination` from input
- Any time you get a `destination`, turn it to false in the map
- Any time you get a `src`, if it already doesn't exist in map, turn it to true

# Code
```cpp
```
![image](https://user-images.githubusercontent.com/10897423/136043134-1bde6d75-1e44-4312-b817-6a912681c77d.png)

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/number-of-employees-under-every-manager-official/ojquestion
