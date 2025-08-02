# Problem Statement

1. You are given two strings s1, s2, and a number K.
2. You have to find if two strings are K-anagrams of each other or not.
3. Two strings are called K-anagrams if

   - Both s1 and s2 have the same number of characters.
   - After changing UPTO K characters in any string, s1 and s2 become anagram of each other.


[Tutorial](https://www.youtube.com/watch?v=VyQbl13RGiw&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=20)

# Thought Process
- Create freq map of s1
- Create freq map of s2
- Take difference/2 of both freq maps (diff = number of characters that are different)

- Instead of two separate freq maps, this can be done in one as shown in the code

# Code
```cpp
void solve(string a, string b , int k) {
    if (a.length() != b.length()) return void(cout << "false");
    map<char, int> freq;

    for (auto i : a) freq[i]++;
    for (auto i : b) freq[i]--;

    int sum = 0;
    for (auto i : freq) {
        if (i.second > 0) sum += i.second;
    }
    cout << (sum <= k ? "true" : "false") << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/k-anagrams-official/ojquestion#!
