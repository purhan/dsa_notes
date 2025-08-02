# Problem Statement
1. You are given a number n and a number m representing number of rows and columns in a maze.
2. You are standing in the top-left corner and have to reach the bottom-right corner. Only two moves are allowed 'h' (1-step horizontal) and 'v' (1-step vertical).
3. Complete the body of getMazePath function - without changing signature - to get the list of all paths that can be used to move from top-left to bottom-right.
Use sample input and output to take idea about output.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=7i41gZLXe5k&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=33)

# Thought Process

# Code
```cpp
// sr - source row
// sc - source column
// dr - destination row
// dc - destination column
vector <string> getMazePaths(int sr, int sc, int dr, int dc) {

    if (sr == dr && sc == dc) {
        vector<string>v;
        v.push_back("");
        return v;
    }

    //for horizontal path
    vector<string> hpath;
    if (sc < dc) {
        hpath = getMazePaths(sr, sc + 1, dr, dc);
    }

    //for vertical path
    vector<string> vpath;
    if (sr < dr) {
        vpath = getMazePaths(sr + 1, sc, dr, dc);
    }

    vector<string> path;
    for (auto& it : hpath) {
        path.push_back("h" + it);
    }

    for (auto& it : vpath) {
        path.push_back("v" + it);
    }

    return path;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-with-arraylists/get-maze-paths-official/ojquestion
