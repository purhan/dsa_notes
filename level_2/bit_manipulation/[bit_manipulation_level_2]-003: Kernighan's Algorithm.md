# Problem Statement

[Tutorial]()

# Thought Process

Rightmost set bit of x => x & ~x

Loop through all rightmost set bits, and flip those bits to count number of set bits

# Code
```cpp
int cnt = 0;

while(n != 0) {
    int rsb = n & ~n;
    n -= rsb;
    cnt++;
}
```

# Problem Links
