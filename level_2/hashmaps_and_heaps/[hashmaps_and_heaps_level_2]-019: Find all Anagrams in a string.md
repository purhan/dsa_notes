# Problem Statement
1. You are given two strings s1 and s2.
2. You have to find the count of s2's anagrams that are present in s1.
3. Also, you have to print the start indices of such anagrams in s1.

[Tutorial](https://www.youtube.com/watch?v=slDyFUnGtoU&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=19)

# Thought Process

Anagram: An anagram is nothing but a permutation of a string. For example: `aabc` and `caba` are anagrams of each other

- Create freq map of `p`
- Create window of `p.length()`
- Put the window at the start of `s`, create freq map of all characters in the window
- Keep sliding the window and adjusting the freq map accordingly
- Whenever freq map of window equals that of `p`, we have an anagram, so increment count

# Code
```cpp
class Solution {
public:
    vector<int> findAnagrams(string s, string p) {
        vector<int> res;
        int l = 0, r = 0;
        map<char, int> freq;

        // find freq of chars in string p
        for(auto i: p) freq[i]++;
        auto freqP = freq;
        freq.clear();

        // create freq map of first size(p) characters in s
        for(; r < p.length(); ++r) {
            char acq = s[r];
            freq[acq]++;
        }
        if(freq == freqP) res.push_back(0);

        // slide window for the rest
        for(; r < s.length(); l++, r++) {
            char acq = s[r];
            freq[acq]++;

            char rel = s[l];
            freq[rel]--;
            if(freq[rel] == 0) freq.erase(rel);

            if(freq == freqP) res.push_back(r - p.length() + 1);
        }

        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/find-all-anagrams-in-a-string
