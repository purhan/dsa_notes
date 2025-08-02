# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=3zyxpFPKkEU&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=18)

# Thought Process
- Question is simple, just heavily dependent on what defines a UTF8 sequence.
- UTF8 numbers can be of 4 types:
  - 1 byte long:
      - Here the first byte will be of the form 0________
  - 2 byte long:
      - Here the first byte will be of the form 110______
      - The second byte will be of the form 10______
  - 3 byte long:
      - First byte of the form 1110____
      - Next two bytes of the form 10______
  - 4 byte long:
      - First byte of the form 11110___
      - Next 3 bytes of the form 10______
- Just check this much

# Code
```cpp
class Solution {
public:
    bool validUtf8(vector<int>& data) {
        int remaining_bytes = 0;

        for(int val: data) {
            if(remaining_bytes == 0) {
                if((val >> 7) == 0b0) {             // first byte of 1 length char
                    remaining_bytes = 0;
                } else if((val >> 5) == 0b110) {    // first byte of 2 length char
                    remaining_bytes = 1;
                } else if((val >> 4) == 0b1110) {   // first byte of 3 length char
                    remaining_bytes = 2;
                } else if((val >> 3) == 0b11110) {  // first byte of 4 length char
                    remaining_bytes = 3;
                } else {
                    return false;
                }
            } else {
                if((val >> 6) == 0b10) remaining_bytes--;
                else return false;
            }
        }
        if(remaining_bytes > 0) return false;

        return true;
    }
};
```

# Problem Links
- https://leetcode.com/problems/utf-8-validation/
