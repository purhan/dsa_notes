# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=UqrcuLv3BnA&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=56)

# Thought Process

# Code
```cpp
class RandomizedSet {
    unordered_map<int, int> itemIdx;
    vector<int> randomList;
public:
    RandomizedSet() {

    }

    bool insert(int val) {
        bool res = (itemIdx.count(val) == 0);
        randomList.push_back(val);
        itemIdx[val] = size(randomList) - 1;
        return res;
    }

    bool remove(int val) {
        bool res = (itemIdx.count(val) > 0);

        if (itemIdx.count(val) > 0) {
            int remIdx = itemIdx[val];
            itemIdx[randomList.back()] = remIdx;
            swap(randomList[remIdx], randomList[size(randomList)-1]);
            itemIdx.erase(val);
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
- https://leetcode.com/problems/insert-delete-getrandom-o1/
