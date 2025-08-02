# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=GbH8PcqKosk&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=26)

# Thought Process
- Take AND with 01010101 and 10101010, then shift both and take their OR

![image](https://user-images.githubusercontent.com/10897423/148671159-769c5504-1ee6-4ba4-a193-c4becec893fa.png)

# Code
```cpp
class Solution {
    public:
    unsigned int swapBits(unsigned int n) {
    	unsigned int oddmask = 0x55555555, evenmask = 0xAAAAAAAA;

    	unsigned int odds = (n & oddmask);
    	unsigned int evens = (n & evenmask);

        odds <<= 1;
        evens >>= 1;

        return (odds | evens);
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/swap-all-odd-and-even-bits-1587115621/1/
