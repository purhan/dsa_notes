# Problem Statement
1. You are given a string.
2. You have to find the length of the longest substring of the given string that contains all non-repeating characters.

[Tutorial](https://www.youtube.com/watch?v=9Kc0eZBGL1U&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=10)

# Thought Process
- Sliding window, simple
- Expand the window while you keep getting unique characters
- If you encoutner a repeating character, contract the window till that character is gone
- Use a map for all this

# Code
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(size(s) == 0) return 0;
        map<char, int> freq;
        int ans = 1;

        int j = 0, i = 0;

        while(j < size(s)) {
            freq[s[j]]++;
            if(freq[s[j]] > 1) {
                while(i < j && freq[s[j]] > 1) {
                    freq[s[i]]--;
                    i++;
                }
            } else {
                ans = max(ans, j - i + 1);
            }
            j++;
        }

        return ans;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/longest-substring-with-unique-characters-official/ojquestion
