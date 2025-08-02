# Problem Statement
1. You are given a number n, representing the count of elements.
2. You are given n numbers.
3. You are given a number "tar".
4. Complete the body of printTargetSumSubsets function - without changing signature - to calculate and print all subsets of given elements, the contents of which sum to "tar". Use sample input and output to get more idea.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=HGDmj5NrrjM&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=49)

# Thought Process

# Code
```cpp
void target_Sum(int* arr, int n, int tar, int curr, string psf) {
    if (n == 0) {
        if (curr == tar) {
            cout << psf << "." << endl;
        }
        return;
    }
    // current array element will be a part
    target_Sum(arr + 1, n - 1, tar, curr + arr[0], psf + to_string(arr[0]) + ",");
    // will not be a part
    target_Sum(arr + 1, n - 1, tar, curr, psf);
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-backtracking/target-sum-subsets-official/ojquestion
