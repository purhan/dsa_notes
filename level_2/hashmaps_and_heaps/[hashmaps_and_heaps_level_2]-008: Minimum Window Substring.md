# Problem Statement

AKA: Smallest Substring Of A String Containing All Characters Of Another String

1. You are given two strings s1 and s2 containing lowercase english alphabets.
2. You have to find the smallest substring of s1 that contains all the characters of s2.
3. If no such substring exists, print blank string("").

[Tutorial](https://www.youtube.com/watch?v=e1HlptlipB0&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=8)

# Thought Process
- Uses acquire release strategy
- Create a freq map of chars in s2
- Start expanding the window from left to right in s1, and create a freq map for s1
- Whenever the condition `freqmap_s1 >= freqmap_s2` is true (i.e. all characters in s2 are present in that substring),
  - Start contracting the window from the left, untill you still have a valid substring
  - When you encounter an invalid substr, continue the expansion again untill you find a valid substr
  - Return the length of the smallest such substr

# Code
```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        string ans = "";

        map<char, int> mapt;
        for(int i = 0; i < t.length(); ++i) {
            mapt[t[i]]++;
        }

        int mct = 0;
        int dmct = t.length();
        map<char, int> maps;
        int i = -1, j = -1;

        while(true) {
            bool f1 = false, f2 = false;

            // acquire
            while(i < int(s.length()) && mct < dmct) {
                i++;
                maps[s[i]]++;

                if(maps[s[i]] <= mapt[s[i]]) {
                    mct++;
                }
                f1 = true;
            }

            // release
            while(j < i && mct == dmct) {
                string pans = s.substr(j + 1, i - j);
                if(ans.length() == 0 || pans.length() < ans.length()) {
                    ans = pans;
                }

                j++;
                if(maps[s[j]] == 1) {
                    maps.erase(s[j]);
                } else {
                    maps[s[j]]--;
                }

                if(maps[s[j]] < mapt[s[j]]) {
                    mct--;
                }
                f2 = true;
            }

            if(f1 == false && f2 == false) {
                break;
            }
        }
        return ans;
    }
};
```

![image](https://user-images.githubusercontent.com/10897423/136190837-10b979d0-bc29-4144-b3bf-2be3e490bf99.png)


# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/smallest-substring-of-a-string-containing-all-characters-of-another-string-official/ojquestion
