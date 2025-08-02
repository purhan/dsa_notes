# Problem Statement
1. You are given a string(str) and a number K.
2. You have to find the length of longest substring of the given string that contains at most K unique characters.

[Tutorial](https://www.youtube.com/watch?v=shsYUyF7pEs&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=18)

# Thought Process
- Uses acquire release strategy
- We start with two pointers, start acquiring characters
- Whenever we acquire more than k characters, we start releasing from the left until we have k unique chars again, then we continue acquiring again and so on
- We take max length of all such valid substrings formed during this process

# Code
```cpp
void solve(string s, int n, int k) {
    map<char, int> freq;

    int ans = 0;
    int l = 0, r = -1;

    while (r < n - 1) {
        r++;
        int acq = s[r];
        freq[acq]++;

        while (freq.size() > k) {
            int rel = s[l];
            freq[rel]--;

            if (freq[rel] == 0) freq.erase(rel);
            l++;
        }

        ans = max(ans, r - l + 1);
    }

    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/longest-substring-with-at-most-k-unique-characters-official/ojquestion#!
