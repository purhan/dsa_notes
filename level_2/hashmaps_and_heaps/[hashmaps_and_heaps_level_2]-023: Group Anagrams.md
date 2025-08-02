# Problem Statement
1. You are given an array of strings.
2. You have to group anagrams together.

[Tutorial](https://www.youtube.com/watch?v=NNBQik4phMI&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=23)

# Thought Process
- Think, you should be able to come up with a solution yourself
- Hint: You just have to create a hashmap of hashmaps

# Code
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        map<map<char, int>, vector<string>> groups;

        for(string str: strs) {
            map<char, int> freq;
            for(char ch: str) {
                freq[ch]++;
            }
            groups[freq].push_back(str);
        }

        vector<vector<string>> res;
        for(auto i: groups) res.push_back(i.second);
        return res;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/group-anagrams-official/ojquestion
- https://leetcode.com/problems/group-anagrams/
