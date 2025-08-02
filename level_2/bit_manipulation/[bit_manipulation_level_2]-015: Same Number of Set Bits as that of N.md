# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=DMTw6pP5zTg&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=17)

# Thought Process
- We do this recursively
- If the current bit is off, we just need to check for possible ways to get k bits in the remaining array
- At each position, if the current bit is set, we need to check for:
    1. possible ways to get (k - 1) bits in the remaining array assuming this bit is always set
    2. possible ways to get (k) bits in the remaining array assuming this bit is off (can be done with simple nCr)

# Code
```cpp
long  solution(long n,long k,int i)
{
    if(i == 0) return 0;
    long mask = (1L << i);

    long res = 0;
    if((n & mask) == 0) {
        // if bit off
        res = solution(n, k, i - 1);
    } else {
        long res1 = solution(n, k - 1, i - 1);
        long res0 = ncr(i, k);
        res = res0 + res1;
    }
    return res;
}
```

# Problem Links
- https://nados.io/content/eb9863ac-63ac-4b94-881f-0aeb24df0985/0c54b191-7b99-4f2c-acb3-e7f2ec748b2a/7fdb0602-0ac9-4484-aff9-a898aed5cd28/f74cfd53-06b7-402e-9065-3f84ef402395/f3e3dbef-d2b7-4f6d-b357-2ef3738e6c91/question/63acf499-ee0c-408e-8dfc-c374d998960d
