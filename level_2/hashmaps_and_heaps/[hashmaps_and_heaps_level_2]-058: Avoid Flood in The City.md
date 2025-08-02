# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138723070-f7449192-49ae-4443-be17-eeadbae7b453.png)

[Tutorial](https://www.youtube.com/watch?v=Q_90h1fxCSM&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=58)

# Thought Process
- For each day, we need to check
  - If that day has already been filled, and on which day it was last filled
  - If there exists a dry day between today and when it was last filled
- We will store everyday, that today, `x` lake is filled, in a map
- If it's a dry day, we will store that day in a set
- Everyday, we will check if this lake has already been filled. If yes, we will search set for a dry day between today and when it was last filled, and update `ans` array accordingly

# Code
```cpp
class Solution {
public:
    vector<int> avoidFlood(vector<int>& rains) {
        int n = rains.size();
        vector<int> ans(n, -1);

        unordered_map<int, int> fulllakes;
        set<int> drydays;

        for(int i = 0; i < n; ++i) {
            int lake = rains[i];

            // 2. If dry day, insert into set
            if(lake == 0) {
                drydays.insert(i);
            } else {

                // 3. else if lake already filled
                if(fulllakes.find(lake) != fulllakes.end()) {

                    // 4. find dry day after lake's previous rain day
                    auto it = drydays.lower_bound(fulllakes[lake]);

                    // 5. If no such rain day, ans={}
                    if (it == drydays.end()) {
                        return {};
                    }

                    // 6. Else, dry this lake on that dry day
                    int dryday = *it;
                    ans[dryday] = lake;
                    drydays.erase(dryday);
                }

                // 1. Store the last day when lake was filled
                fulllakes[lake] = i;
            }
        }

        // 7. Shenanigan, dont mind this code
        for(auto day: drydays) {
            ans[day] = 1;
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/avoid-flood-in-the-city/
