# Problem Statement
1. You are given a number n and a number m representing number of rows and columns in a maze.
2. You are standing in the top-left corner and have to reach the bottom-right corner. Only two moves are allowed 'h' (1-step horizontal) and 'v' (1-step vertical).
3. Complete the body of pri tMazePath function - without changing signature - to print the list of all paths that can be used to move from top-left to bottom-right.
Use sample input and output to take idea about output.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=TcCyI-eJMmY&list=TLGGvq5Jn0dlMMgwMTEwMjAyMQ)

# Thought Process

# Code
```cpp
void printMazePaths(int sr, int sc, int dr, int dc, string psf) {
    if (sr > dr || sc > dc) {
        return;
    }

    if (sr == dr && sc == dc) {
        cout << psf << endl;
        return;
    }

    printMazePaths(sr, sc + 1, dr, dc, psf + "h");
    printMazePaths(sr + 1, sc, dr, dc, psf + "v");
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-on-the-way-up/print-maze-paths-official/ojquestion
