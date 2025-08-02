# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=7LmgzOCnZQk&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=53) tutorial wasnt good

[LC Article](https://leetcode.com/problems/furthest-building-you-can-reach/discuss/918373/O(nlogn)-Greedy-approach-using-a-min-heap-to-maintain-the-num(ladders)-of-largest-gaps.)

# Thought Process
- You can think of this problem as a variant of `K largest elements`, or maybe `smallest index from start, which includes all K largest elements`
- For whatever distance we can reach, we will use ladders for the tallest ones and bricks for the shortest ones (easy greedy)
- We will traverse through buildings, we don't need to jump on buildings that are smaller than previous
- We will fill a min_heap of all jump heights
- When min_heap's size crosses number of ladders, we will start using bricks for the smallest of those min_heap's jumps
- Naturally, when we exhaust our bricks, the `L` largest jumps will remain in heap, where L = number of Ladders. So you can think of this problem as a variant of `K largest elements`

# Code
```cpp
class Solution {
public:
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        int n = size(heights);
        priority_queue<int, vector<int>, greater<int>> pq;

        for(int i = 1; i < n; ++i) {
            if(heights[i] <= heights[i - 1]) continue;

            pq.push(heights[i] - heights[i - 1]);

            // We can definitely take atleast `ladders` jumps
            if(pq.size() > ladders) {

                // when we exceed more jumps than `ladders`, we have to use bricks for the smallest of those jumps
                int cost = pq.top(); pq.pop();
                bricks -= cost;
            }
            if(bricks < 0) return i - 1;
        }
        return n - 1;
    }
};
```

# Problem Links
- https://leetcode.com/problems/furthest-building-you-can-reach/
