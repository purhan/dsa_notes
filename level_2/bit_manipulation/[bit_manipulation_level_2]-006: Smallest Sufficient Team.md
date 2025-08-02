# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=5gXNMGiqQbU&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=6)

# Thought Process
REVISE THIS!!!!

# Code
```cpp
class Solution {
public:
    vector<int> v;
    map<string,int> mp;
    int n; int m;
    int x;
    vector<int> pp;

    void fun(int id,int s,vector<int>& us){
        if(s >= x){
            // v.size() < 1 to take where when the vector v is empty then it's size is 0
            if(us.size() < v.size() || v.size() < 1){
                v = us;
            }
            return;
        }
        // to limit the no of recursive calls
        if(id == n ||(v.size()>0 && us.size() >= v.size()))
            return;

        int i;
        // if the ith skill is already included in the current s
        if(s & (1 << id))
            fun(id+1,s,us);
        else{
            // For every person which has that skill, we wouls try to recurr.
            for(i=0;i<m;i++){
                if(pp[i] & (1 << id)){
                    int p = s | pp[i];
                    us.push_back(i);
                    fun(id+1,p,us);
                    us.pop_back();
                }
            }
        }
    }
    vector<int> smallestSufficientTeam(vector<string>& skills, vector<vector<string>>& pep) {
        n=skills.size();
        m=pep.size();

        int i,j;x=1;
        // storing every skill as key-value pair

        for(i=0;i<n;i++){
            mp[skills[i]]=i;
            x *= 2;
        }
        x--; // The desired value when every skill would be included

        for(i=0;i<m;i++){
            int y=0;// stores the dcimal representation of every person skills

            for(j=0;j<pep[i].size();j++){
                y += (1 << mp[pep[i][j]]);
            }
            pp.push_back(y);
        }

        vector<int> bb;
        fun(0,0,bb);
        return v;
    }
};

```

# Problem Links
- https://leetcode.com/problems/smallest-sufficient-team/
