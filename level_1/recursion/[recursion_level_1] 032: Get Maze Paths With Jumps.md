# Problem Statement
1. You are given a number n and a number m representing number of rows and columns in a maze.
2. You are standing in the top-left corner and have to reach the bottom-right corner.
3. In a single move you are allowed to jump 1 or more steps horizontally (as h1, h2, .. ), or 1 or more steps vertically (as v1, v2, ..) or 1 or more steps diagonally (as d1, d2, ..).
4. Complete the body of getMazePath function - without changing signature - to get the list of all paths that can be used to move from top-left to bottom-right.
Use sample input and output to take idea about output.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=F6T3tD8Pw20&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=32)

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

    vector<string>path;
    vector<string> hpath;
    if (sc < dc) {
        for (int i = 1; i <= dc; i++) {
            hpath = getMazePaths(sr, sc + i, dr, dc);
            for (auto& it : hpath) {
                path.push_back("h" + to_string(i) + it);
            }
        }
    }

    vector<string> vpath;
    if (sr < dr) {
        for (int i = 1; i <= dr; i++) {
            vpath = getMazePaths(sr + i, sc, dr, dc);
            for (auto& it : vpath) {
                path.push_back("v" + to_string(i) + it);
            }
        }
    }

    vector<string> dpath;
    if (sr < dr && sc < dc) {
        for (int i = 1; i <= dr && i <= dc; i++) {
            dpath = getMazePaths(sr + i, sc + i, dr, dc);
            for (auto& it : dpath) {
                path.push_back("d" + to_string(i) + it);
            }
        }
    }

    return path;
}

void display(vector<string>& arr) {
    cout << "[";
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i];
        if (i < arr.size() - 1) cout << ", ";
    }

    cout << "]" << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-with-arraylists/get-maze-path-with-jumps-official/ojquestion