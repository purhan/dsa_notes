# Problem Statement
1. You are required to complete the code of our MedianPriorityQueue class. The class should mimic the behaviour of a PriorityQueue and give highest priority to median of it's data.
2. Here is the list of functions that you are supposed to complete
2.1. add -> Should accept new data.
2.2. remove -> Should remove and return median value, if available or print "Underflow" otherwise and return -1
2.3. peek -> Should return median value, if available or print "Underflow" otherwise and return -1
2.4. size -> Should return the number of elements available
3. Input and Output is managed for you.

Note -> If there are even number of elements in the MedianPriorityQueue, consider the smaller median as median value.

[Tutorial](https://www.youtube.com/watch?v=dshWERdcAdg&list=PL-Jc9J83PIiHq5rMZasunIR19QG3E-PAA&index=18)

# Thought Process
- Take two priority queues, one sorts ascending, other sorts descending
- At any point, we will store almost half elements in each pq. If one pq has n elements, other will have at most n + 1 or n elements
- If one pq exceeds this, we will rearrange them (read the code to understand)

# Code
```cpp
#include <bits/stdc++.h>
using namespace std;

class MedianPQ {
    priority_queue<int, vector<int>, greater<int>> right;
    priority_queue<int> left;

public:
    void add(int n) {
        if (right.size() != 0 && right.top() <= n) {
            right.push(n);
        } else {
            left.push(n);
        }

        if ((int)(left.size() - right.size()) > 1) {
            right.push(left.top());
            left.pop();
        }
        else if ((int)(right.size() - left.size()) > 1) {
            left.push(right.top());
            right.pop();
        }
    }

    int remove() {
        if (this->size() == 0)
            return -1;
        int res = 0;
        if (left.size() >= right.size()) {
            res = left.top();
            left.pop();
        } else if (right.size() > left.size()) {
            res = right.top();
            right.pop();
        }
        return res;
    }

    int peek() {
        if (this->size() == 0)
            return -1;
        if (left.size() >= right.size())
            return left.top();
        else
            return right.top();
    }

    int size() {
        return left.size() + right.size();
    }
};

int main() {
    MedianPQ mpq;
    while (true) {
        string str; cin >> str;
        if (str == "quit") {
            break;
        } else if (str == "add") {
            int n; cin >> n;
            mpq.add(n);
        } else if (str == "remove") {
            cout << mpq.remove() << endl;
        } else if (str == "peek") {
            cout << mpq.peek() << endl;
        } else if (str == "size") {
            cout << mpq.size() << endl;
        }
    }
    return 0;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/hashmap-and-heap/median-priority-queue-official/ojquestion
