# Problem Statement

You are given a list of strings from the alien language's dictionary, where the strings in words are sorted lexicographically by the rules of this new language.
Return a string of the unique letters in the new alien language sorted in lexicographically increasing order by the new language's rules. If there is no solution, return "". If there are multiple solutions, return any of them.

[Tutorial](https://www.youtube.com/watch?v=_u1Mn4_2hIo&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=14)

# Thought Process
- For any 2 consecutive words in a dictionary, we can only compare the first 2 distinct characters from the left
- For every 2 consecutive words, we construct a graph of letters that are different in those words. That means, letter a1 should come before letter a2
- Topological sorting of the graph is the ans

# Code
```cpp
void dfs(char v) {
    visited[v] = true;
    for (auto u : adj[v]) {
        if (!visited[u])
            dfs(u);
    }
    ans.push_back(v);
}

void topological_sort() {
    for (auto [c, v] : adj) {
        if (!visited[c])
            dfs(c);
    }
    reverse(ans.begin(), ans.end());
}

void findFirstDiffChar(string s1, string s2) {
    int m = min(s1.length(), s2.length());
    for (int i = 0; i < m; ++i) {
        if (s1[i] != s2[i]) {
            adj[s1[i]].push_back(s2[i]);
            return;
        }
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/alien-dictionary-official/ojquestion#!
