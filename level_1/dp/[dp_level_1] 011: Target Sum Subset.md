# Problem Statement
1. You are given a number n, representing the count of elements.
2. You are given n numbers.
3. You are given a number "tar".
4. You are required to calculate and print true or false, if there is a subset the elements of which add 
     up to "tar" or not.

Duplication NOT allowed

# Thought Process

Recursive:
- Uses include exclude principle. We can either use this coin in the sum, or not use it
- If we use it, we need to check for `target - nums[i]` in the remaining coins (We traverse from left to right so we can just use a pointer to check for remaining coins)
- If we dont use it, just check for `target` in the remaining array

Iterative:
- Idea obviously same as recursive

![image](https://user-images.githubusercontent.com/10897423/140935970-110812d8-6d3f-451b-9373-2fe3f5b496e1.png)

# Code

Recursive:

```cpp
bool canReach(vector<int> nums, int target, int i, map<pair<int, int>, bool>& mem) {
    if (mem.count({i, target})) return mem[ {i, target}];
    if (i >= (int)nums.size()) return false;
    else if (nums[i] == target) return true;

    return mem[ {i, target}] = canReach(nums, target, i + 1, mem)
                               ||
                               canReach(nums, target - nums[i], i + 1, mem);
}
```

Iterative:

```cpp
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/target-sum-subsets-dp-official/ojquestion#!
