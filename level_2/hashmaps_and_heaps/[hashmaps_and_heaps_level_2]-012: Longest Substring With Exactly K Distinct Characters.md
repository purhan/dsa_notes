# Problem Statement
1. You are given a string(str) and a number K.
2. You have to find length of the longest substring that has exactly k unique characters.
3. If no such substring exists, print "-1".

[Tutorial](https://www.youtube.com/watch?v=SIh3RfFPQwU&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=12)

# Thought Process
- Similar to previous fre problems. Uses acquire release strategy
- Start expanding window and store elements in a map untill you get `k` unique characters in that map
- When you get more than `k`, start contracting the window until either the window is collapsed (i == j) or no_of_unique_elements is `k` again

> Remember to do `Count Substrings with exactly K distinct characters`, BECAUSE it's much different actually

# Code
```cpp
```

![image](https://user-images.githubusercontent.com/10897423/136217960-ba42033b-5af8-4148-a71b-39cc14b7fd33.png)

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/longest-substring-with-exactly-k-unique-characters-official/ojquestion
