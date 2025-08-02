# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=v7pUZw-ZOYU&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=22)

# Thought Process
- Create a mask in left to right range
- mask in that range contains only 1's
- AND operation of mask with A gives us the bits we need to copy
- OR operation of mask with B gives us the answer

- Investigate how to create the mask (read the code)

# Code
```cpp
void solve(int a, int b, int l, int r) {
    int mask = 1;                   // 000000000000000000000000000001
    mask = (mask << (r - l + 1));   // 000000000000000000000001000000
    mask--;                         // 000000000000000000000000111111
    mask = (mask << (l - 1));       // 000000000000000000111111000000

    mask = (mask & a);
    cout << (mask | b) << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/bit-manipulation/copy-set-bits-in-a-range-official/ojquestion#!
