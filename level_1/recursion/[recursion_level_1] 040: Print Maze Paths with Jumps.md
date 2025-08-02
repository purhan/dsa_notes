# Problem Statement

[Tutorial](https://www.youtube.com/watch?list=TLGGv6_bg6nVfcAwMTEwMjAyMQ&v=LgFl0hsyWP8&feature=emb_imp_woyt)

# Thought Process

# Code
```cpp
void printMazePaths(int sr, int sc, int dr, int dc, string psf) {
    // write your code here

    if (sr > dr || sc > dc) {
        return;
    }

    if (sr == dr && sc == dc ) {
        cout << psf << endl;
        return;
    }

    //can make column wise jump(horizontal)
    for (int i = 1; i <= dc; i++) {
        printMazePaths(sr, sc + i, dr, dc, psf + "h" + to_string(i));
    }

    //can make row wise jump(vertical)
    for (int i = 1; i <= dr; i++) {
        printMazePaths(sr + i, sc, dr, dc, psf + "v" + to_string(i));
    }

    //can make diagonal jump
    for (int i = 1; i <= dr && i <= dc; i++) {
        printMazePaths(sr + i, sc + i, dr, dc, psf + "d" + to_string(i));
    }

}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-on-the-way-up/print-maze-path-with-jumps-official/ojquestion
