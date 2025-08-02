# Problem Statement


[Tutorial](https://www.youtube.com/watch?v=hMJAlbJIS7E&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=29)

# Thought Process

# Code
```cpp
vector<string> getStairsPath(int n) {
    if (n <= 0) {
        vector<string> v;
        v.push_back("");
        return v;
    }

    vector<string> path3 = getStairsPath(n - 1);
    vector<string> path2 = getStairsPath(n - 2);
    vector<string> path1 = getStairsPath(n - 3);

    vector<string> finalpath;

    if (n >= 1) {
        for (auto& it : path3) {
            finalpath.push_back(to_string(1) + it);
        }
    }

    if (n >= 2) {
        for (auto& it : path2) {
            finalpath.push_back(to_string(2) + it);
        }
    }


    if (n >= 3) {
        for (auto& it : path1) {
            finalpath.push_back(to_string(3) + it);
        }
    }
    return finalpath;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-with-arraylists/get-kpc-official/ojquestion
