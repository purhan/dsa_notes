# Problem Statement

In a given cartesian plane, there are N points. We need to find the Number of Pairs of  points(A, B) such that

    - Point A and Point B do not coincide.
    - Manhattan Distance and the Euclidean Distance between the points should be equal.


[Tutorial](https://www.youtube.com/watch?v=7UVJYPT3-uI&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=59)

# Thought Process

# Code
```cpp
class Solution {
  public:
    int numOfPairs(int X[], int Y[], int N) {
        map<int, int> x, y;             // count repeating x, count repeating y.
        map<pair<int, int>, int> xy;    // count duplicate points

        int ans = 0;

        for(int i = 0; i < N; ++i) {

            if(x[X[i]] > 0) ans += x[X[i]];                         // find number of pairs with same x
            if(y[Y[i]] > 0) ans += y[Y[i]];                         // find number of pairs with same y
            if(xy[{X[i], Y[i]}] > 0) ans -= 2 * xy[{X[i], Y[i]}];   // duplicate points were counted twice, so subtract them

            x[X[i]]++;
            y[Y[i]]++;
            xy[{X[i], Y[i]}]++;
        }

        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/pairs-of-non-coinciding-points4141/1
