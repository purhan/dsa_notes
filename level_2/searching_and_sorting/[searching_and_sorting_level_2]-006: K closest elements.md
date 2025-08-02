# Problem Statement
1. Given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.
2. An integer a is closer to x than an integer b if:

        |a - x| < |b - x|, or
        |a - x| == |b - x| and a < b

[Tutorial](https://www.youtube.com/watch?v=1otAwCQG7XM&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=6)

> THIS IS UNOPTIMIZED, Check next file for optimized solution

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134775285-df31a325-bd2e-4c16-85e3-2c58189c9aec.png)

- In a separate array `gap`, store the difference of each element with `x`.
- Write a comparator to sort based on that gap
- No need to sort all elements since we have to find only `k` closest
- So use priority queue of size `k` in this case
- Traverse and fill the priority queue. By the end, you will have only k closest elements in that queue

# Code

> Code is flawed!!!

```cpp
class CompareDist
{
public:
    bool operator()(pair<int,int> n1, pair<int,int> n2) {
        if(n1.first == n2.first) {
            return n1.second - n2.second;
        }
        return n1.first < n2.first;
    }
};

class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        int n = size(arr);
        vector<int> gaps(n);

        for(int i = 0; i < n; ++i) {
            gaps[i] = abs(arr[i] - x);    
        }
        
        priority_queue<pair<int, int>, vector<pair<int, int>>, CompareDist> pq;
        for(int i = 0; i < n; ++i) {
            pq.push({gaps[i], arr[i]});
            if(size(pq) > k) pq.pop();
        }
        
        vector<int> res;
        while(!pq.empty()) {
            auto t = pq.top();
            res.push_back(t.second);
            pq.pop();
        }
        return res;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find_k_closest_elements/ojquestion#!
- https://leetcode.com/problems/find-k-closest-elements/
