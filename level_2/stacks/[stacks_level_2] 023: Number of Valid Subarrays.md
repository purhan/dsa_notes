# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=P0Fz-ZIVY5k&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=24)

# Thought Process
- At every index, find out the next smaller element
- Till that smaller element only, can we create a valid subarray

# Code
```cpp
int validSubarrays(vector<int> nums){
    int n = nums.size();
    int ans = 0;
    stack<int> st;

    for(int i = n - 1; i >= 0; --i) {
        while(!st.empty() && nums[i] <= nums[st.top()]) {
            st.pop();
        }
        int nextSmallerElement = ((st.empty()) ? -1 : st.top());
        if(nextSmallerElement == -1) {
            ans += (n - i);
        } else {
            ans += nextSmallerElement - i;
        }
        st.push(i);
    }
    return ans;
}
```

# Problem Links
- https://nados.pepcoding.com/content/eb9863ac-63ac-4b94-881f-0aeb24df0985/0c54b191-7b99-4f2c-acb3-e7f2ec748b2a/7fdb0602-0ac9-4484-aff9-a898aed5cd28/d108313e-68c8-4fc6-bb02-6e9a9010ef9e/8c6022a5-8654-4226-918f-8110af738bd4/question/0d5aa694-b447-45d7-8e36-878a1ba58cc9
