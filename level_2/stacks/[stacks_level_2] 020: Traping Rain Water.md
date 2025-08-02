# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=E9ziS6Fb2nw&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=20)

# Thought Process
- Can also be solved using 2 different approaches (Search notes), Intuition is same tho. Next video also has another approach using 2 pointers
- Use stack to check the immediate left and right barriers of a column
- Assuming water till that height, add that to the answer. The answer will be somehow correct, dont know how to explain. Look at screenshots

![image](https://user-images.githubusercontent.com/10897423/147814990-d1cfa476-25de-497d-8e8d-60d2e4f2710a.png)

![image](https://user-images.githubusercontent.com/10897423/147815005-41496b36-7ec8-44e8-9123-1c8413f588ad.png)


# Code
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n = height.size(), ans = 0;
        stack<int> st;

        for(int i = 0; i < n; ++i) {
            while(!st.empty() && height[st.top()] <= height[i]) {
                int rightBarrier = i;
                int curHeight = height[st.top()]; st.pop();
                if(st.empty()) break;
                int leftBarrier = st.top();

                int width = rightBarrier - leftBarrier - 1;
                ans += (min(height[rightBarrier], height[leftBarrier]) - curHeight) * width;
            }
            st.push(i);
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/trapping-rain-water/
