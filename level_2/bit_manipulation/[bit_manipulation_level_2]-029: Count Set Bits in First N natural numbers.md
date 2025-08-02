# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=g6OxU-hRGtY&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=29)

# Thought Process
- Find largest power of 2 that is just smaller than that number
- Till the power of 2, number of bits = `2^(x-1) * x`

![image](https://user-images.githubusercontent.com/10897423/148679147-fb70be3b-e68b-45ed-8d78-f1b4878c92e9.png)

- For the remaining numbers, we have the most significant bit on in each number, so just add the count of remaining numbers to the answer
- Finally, the remaining bits in the remaining numbers can be found out recursively using solve(n-x)

![image](https://user-images.githubusercontent.com/10897423/148679086-574041cd-5a64-4265-8f1f-105b97e08096.png)


# Code
```cpp
class Solution{
    int powerOf2(int n) {
        int x = 0;
        while((1 << x) <= n) {
            x++;
        }
        return x - 1;
    }
public:
    int countBits(int N){
        if(N <= 2) return N;
        int x = powerOf2(N);

        // bits till largest power of 2 that is less than N
        int ans = (1 << (x - 1)) * x;

        // bits in remaining numbers
        ans += (N - (1 << x) + 1) + countBits(N - (1 << x));

        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/sherlock-and-his-enemies2304/1/#
