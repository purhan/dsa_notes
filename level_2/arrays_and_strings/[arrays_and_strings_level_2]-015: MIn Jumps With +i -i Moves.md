# Problem Statement
1. Given an integers X. 
2. The task is to find the minimum number of jumps to reach a point X in the number line starting from zero.
3. The first jump made can be of length one unit and each successive jump will be exactly one unit longer than the previous jump in length. 
4. It is allowed to go either left or right in each jump.

[Tutorial](https://www.youtube.com/watch?v=fsips_0hwEA&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=15)

# Thought Process
- First, keep taking jumps till your position exceeds/coincides target
- Now check difference between position and target
- If diff is even, we need one less jump, i.e. one jump had to be reversed (think)
- If diff is odd, check if next jump would make it even. If yes, then ans is jump+1, else ans is jump+2 since the one after that is guaranteed to make diff even

# Code
```cpp
void solve(int x) {
    int jump = 0, sum = 0;

    while (sum < x) {
        jump++;
        sum += jump;
    }

    if ((sum - x) % 2 == 0) {
        cout << jump << endl;
    } else if ((sum + jump + 1 - x) % 2 == 0) {
        cout << jump + 1 << endl;
    } else {
        cout << jump + 2 << endl;
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/arrays-and-strings/min_jumps_with_+i_-i_moves/ojquestion
