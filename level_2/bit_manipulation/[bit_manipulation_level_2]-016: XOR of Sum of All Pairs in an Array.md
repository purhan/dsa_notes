# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=10sMnEraOBs&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=16)

# Thought Process
- Thing to observe here:

![image](https://user-images.githubusercontent.com/10897423/148558295-3a1889d4-debe-4939-8c46-bd60001c339e.png)

# Code
```cpp
int solution(vector<int> &v1)
{
    int ans = 0;
    for(auto i: v1) ans ^= (2 * i);
    return ans;
}
```

# Problem Links
- https://nados.io/content/eb9863ac-63ac-4b94-881f-0aeb24df0985/0c54b191-7b99-4f2c-acb3-e7f2ec748b2a/7fdb0602-0ac9-4484-aff9-a898aed5cd28/f74cfd53-06b7-402e-9065-3f84ef402395/f3e3dbef-d2b7-4f6d-b357-2ef3738e6c91/question/210129c9-abee-439f-88f6-02e4b2a949b8
