# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138561107-5406e329-e69c-4312-8505-30e00a30879b.png)

[Tutorial](https://www.youtube.com/watch?v=a-UYY_DvCBY&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=56)

# Thought Process

# Code
```cpp
class RandomizedCollection {
    unordered_map<int, set<int>> itemIdx;       // stores index of each item (even duplicates!)
    vector<int> randomList;                     // our actual array. Slow, that's why we have the map above
public:

    bool insert(int val) {
        bool res = (itemIdx.count(val) == 0);
        randomList.push_back(val);                  // Simply push in array
        itemIdx[val].insert(size(randomList) - 1);  // and store its index
        return res;
    }

    bool remove(int val) {
        bool res = (itemIdx.count(val) > 0);

        if (itemIdx.count(val) > 0) {
            int remIdx = *itemIdx[val].rbegin();                        // take index of item to be removed
            itemIdx[randomList.back()].erase(randomList.size() - 1);    // change index of last item of array
            itemIdx[randomList.back()].insert(remIdx);
            swap(randomList[remIdx], randomList[size(randomList)-1]);   // swap with last item, then pop
            itemIdx[val].erase(remIdx);
            if(itemIdx[val].size() == 0) itemIdx.erase(val);
            randomList.pop_back();
        }

        return res;
    }

    int getRandom() {
        int idx = rand() % randomList.size();
        return randomList[idx];
    }
};
```

# Problem Links
- https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/
