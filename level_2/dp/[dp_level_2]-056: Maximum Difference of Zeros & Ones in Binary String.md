# Problem Statement

1. You are given a string containing only 0's and 1's.

2. You have to find the length of substring which is having maximum difference of number of 0s and number of 1s i.e (Number of 0's - Number of 1's).

3. If there are all 1's present in the given string, then print '-1'. 

[Tutorial](https://www.youtube.com/watch?v=_k_Codwq1ls&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=56)

# Thought Process
- Inspired by Kadane's
- If found 0, we increment current sum
- If found 1, we decrement current sum
- If current sum is ever negative, we discard array till that index and cursum=0

# Code
```cpp
void solve(string s) {
    int n = s.size();

    int cursum = 0, ans = -1;
    for (int i = 0; i < n; ++i) {
        if (s[i] == '0') cursum++;
        else cursum--;

        if (cursum < 0) cursum = 0;

        ans = max(ans, cursum);
    }

    cout << ans << endl;
}
```

# Problem Links
- https://nados.pepcoding.com/content/eb9863ac-63ac-4b94-881f-0aeb24df0985/0c54b191-7b99-4f2c-acb3-e7f2ec748b2a/7fdb0602-0ac9-4484-aff9-a898aed5cd28/f74cfd53-06b7-402e-9065-3f84ef402395/5539a6e8-c8bf-4f04-805c-e43e9d20e72a/question/0be128f4-0d29-4fa7-aad5-e3bcfb61da02
