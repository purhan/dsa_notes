# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/137370337-01dc1711-b50b-4637-8233-60b591789361.png)

[Tutorial](https://www.youtube.com/watch?v=4ndmX1FvZks&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=47)

# Thought Process
- Nothing, just implementation is all that matters since its difficult in cpp

# Code
```cpp
class Solution {
public:
    vector<string> subdomainVisits(vector<string>& cpdomains) {
        vector<string> ans;

        map<string, int> cnt;
        for(string str: cpdomains) {


            // parse frequency and domain
            int freq = stoi(str.substr(0, str.find(" ")));
            string domain = str.substr(str.find(" ") + 1);

            // store freq for domain
            cnt[domain] += freq;

            // store freq for all sub-domains
            for(int i = 0; i < domain.length(); ++i) {
                if(domain[i] == '.') {
                    string sub_domain = domain.substr(i + 1);
                    cnt[sub_domain] += freq;
                }
            }
        }

        for(auto [sub_d, f] : cnt) {
            string i = to_string(f) + " " + sub_d;
            ans.push_back(i);
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/powerful-integers/
