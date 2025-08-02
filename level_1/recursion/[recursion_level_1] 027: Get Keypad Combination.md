# Problem Statement
1. You are given a string str. The string str will contains numbers only, where each number stands for a key pressed on a mobile phone.
2. The following list is the key to characters map :
```
    0 -> .;
    1 -> abc
    2 -> def
    3 -> ghi
    4 -> jkl
    5 -> mno
    6 -> pqrs
    7 -> tu
    8 -> vwx
    9 -> yz
```
4. Complete the body of getKPC function - without changing signature - to get the list of all words that could be produced by the keys in str.
Use sample input and output to take idea about output.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=3fjt19bjs3A&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=27)

# Thought Process

# Code
```cpp
vector<string> letterCombinationsHelper(string digits, vector<string> bag) {
    if (digits.length() == 0) {
        vector<string> s;
        s.push_back("");
        return s;
    }

    int index = digits[0] - '0';
    string small = bag[index];
    string ros = digits.substr(1);
    vector<string> smalloutput = letterCombinationsHelper(ros, bag);
    vector<string> output;
    for (int i = 0; i < (int)small.length(); i++) {
        for (auto& it : smalloutput) {
            output.push_back(small[i] + it);
        }
    }
    return output;
}

vector<string> letterCombinations(string digits) {
    vector<string> bag{".;", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tu", "vwx", "yz"};
    return letterCombinationsHelper(digits, bag);
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-with-arraylists/get-kpc-official/ojquestion
