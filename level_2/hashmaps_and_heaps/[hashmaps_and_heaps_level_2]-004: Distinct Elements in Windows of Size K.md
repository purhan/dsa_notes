# Problem Statement
1. You are given an array(arr) of integers and a number K.
2. You have to find the count of distinct numbers in all windows of size k.

[Tutorial](https://www.youtube.com/watch?v=x8O9XocEioI&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=4)

# Thought Process
- Uses "acquire release strategy"
- Create sliding window of size k
- Move window. With every move, add new acquired elements to frequency map `freq`, and reduce the frequency of elements on the left (the ones you just released)
- If on release, frequency becomes 0, just erase that element
- Keep printing the size of map with every move as the problem asks

# Code

![image](https://user-images.githubusercontent.com/10897423/136059716-4f9e78bb-bc80-4a09-9e02-2626bbb1b3eb.png)

```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/count-distinct-elements-in-every-window-of-size-k-official/ojquestion
