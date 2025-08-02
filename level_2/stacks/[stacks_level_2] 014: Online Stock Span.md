# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=LAGvGrd2lcE&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=14)
[Tutorial2](https://www.youtube.com/watch?v=0BsPlzqksZQ)

# Thought Process
- Just implementation

# Code
```cpp
class StockSpanner {
public:
    StockSpanner() {}

    stack<pair<int, int>> s;

    int next(int price) {
        int day = 1;

        while(!s.empty() && s.top().first <= price) {
            day += s.top().second;
            s.pop();
        }
        s.push({price, day});

        return day;
    }
};
```

# Problem Links
- https://leetcode.com/problems/online-stock-span/
