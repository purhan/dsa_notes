# Problem Statement

There is a line that goes through the points p1=(x1,y1) and p2=(x2,y2). There is also a point p3=(x3,y3).

Your task is to determine whether p3 is located on the left or right side of the line or if it touches the line when we are looking from p1 to p2.

[Tutorial](https://www.youtube.com/watch?v=Twcp9Vdq88Y&list=PL-Jc9J83PIiH0l9IZvdeC55dbFQpdMDSS)

# Thought Process
- Find slope between both pairs of points and check if its clockwise, anticlockwise or not changing

# Code
```cpp
void solve() {
    int x1, x2, x3, y1, y2, y3;
    cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;

    int val = (x3 - x2) * (y2 - y1) - (x2 - x1) * (y3 - y2);
    if (val < 0) {
        cout << "LEFT" << endl;
    } else if (val > 0) {
        cout << "RIGHT" << endl;
    } else {
        cout << "TOUCH" << endl;
    }
}
```

# Problem Links
- https://cses.fi/problemset/task/2189/
