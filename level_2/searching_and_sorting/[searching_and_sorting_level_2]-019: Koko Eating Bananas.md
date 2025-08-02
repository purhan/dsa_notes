# Problem Statement
1. Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.
2. Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.
3. Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.
4. Return the minimum integer k such that she can eat all the bananas within h hours.

[Tutorial](https://www.youtube.com/watch?v=LzZFUTWE55c&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=19)

# Thought Process
- Maximum time koko takes is *max_element(array)
- So we do a binary search in 0->max_time
- Whenever the condition is satisfied, we continue searching in less time range, else return our answer

# Code
```cpp
class Solution {
    bool isPossibleToEat(vector<int>& piles, int speed, int h) {
        if(speed == 0) return false;
        int time = 0;
        for(auto i: piles) {
            time += i / speed;
            if(i % speed > 0) time++;
        }

        return (time <= h);
    }
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int lo = 0, hi = *max_element(piles.begin(), piles.end());
        int speed = hi;

        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            if(isPossibleToEat(piles, mid, h)) {
                hi = mid - 1;
                speed = mid;
            } else {
                lo = mid + 1;
            }
        }

        return speed;
    }
};
```

# Problem Links
- https://leetcode.com/problems/koko-eating-bananas/
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/koko_eating_bananas/ojquestion
