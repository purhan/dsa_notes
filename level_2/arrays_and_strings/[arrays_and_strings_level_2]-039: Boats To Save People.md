# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138467841-37994348-8a61-42ef-a9ca-882513a64fe6.png)

[Tutorial](https://www.youtube.com/watch?v=_KRgvkkxTzQ&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=39)

# Thought Process
- Sort, then 2 pointer
- First sort
- Use 2 pointers to check if 2 selected people can sit in the same boat.
  - If yes, both sit in same boat. Increase count by 1, move both pointers
  - If no, bigger person requires one boat for himself. Increase count by 1, decrease right pointer
- Edge case, both pointers end up at same position in the end. For that, make sure the condition in while loop is i<=j

# Code
```cpp
class Solution {
public:
    int numRescueBoats(vector<int>& people, int limit) {
        int n = people.size();
        sort(people.begin(), people.end());
        int i = 0, j = n - 1, ans = 0;

        while(i <= j) {
            if(people[i] + people[j] <= limit) {
                ans++;
                i++;
                j--;
            } else {
                ans++;
                j--;
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/boats-to-save-people/
