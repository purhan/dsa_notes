# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/137474399-5beaaca1-3fa1-48db-a1bd-5935111529a0.png)

[Tutorial](https://www.youtube.com/watch?v=JxtmaAFfVBo&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=50)

# Thought Process

# Code
```cpp
class LRUCache {
public:

    list<pair<int, int>> cache;
    int cache_capacity;
    unordered_map<int, list<pair<int, int>>::iterator> m;   // key = element, value = its position in list

    LRUCache(int capacity) {
        cache_capacity = capacity;
    }

    int get(int key) {

        // If doesnt exist, return -1;
        if(m.find(key) == m.end()) return -1;

        // Else

        // Take that key, move it to the begining;
        cache.splice(cache.begin(), cache, m[key]); // splice(position_to_place_at, list_to_get_it_from, the_element_itself)

        // Return its value;
        return m[key]->second;
    }

    void put(int key, int value) {

        // If already exists, dont put, just move to front of the list and update value;
        if(m.find(key)!=m.end()) {
            cache.splice(cache.begin(), cache, m[key]);
            m[key]->second = value;
            return;
        }

        if(cache.size()==cache_capacity) {
            auto d_key=cache.back().first;
            cache.pop_back();
            m.erase(d_key);
        }
        cache.push_front(make_pair(key, value));
        m[key] = cache.begin();
    }
};
```

# Problem Links
- https://leetcode.com/problems/lru-cache/