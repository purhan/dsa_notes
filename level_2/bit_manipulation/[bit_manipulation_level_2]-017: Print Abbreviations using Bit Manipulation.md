# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=2F-c8F4TCOo&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=18)

# Thought Process
- We'll have 2^n results where n is the length of the string
- We traverse over 1 to (1 << n)
- For each number, we will check the bits of that number
- Whereever bits are off, we will print the char, if bits are on, we will increment the counter

# Code
```cpp
void solve(string str) {
    for(int i = 0; i < (1 << str.length()); ++i) {
        int cnt = 0;
        string res = "";

        for(int j = 0; j < str.length(); ++j) {
            int bit = str.length() - j - 1;

            if((i & (1 << bit)) == 0) {
                if(cnt == 0) {
                    res += str[j];
                } else {
                    res += to_string(cnt);
                    res += str[j];
                    cnt = 0;
                }
            } else {
                cnt++;
            }
        }
        if(cnt > 0) res += to_string(cnt);
        cout << res << endl;
    }
}
```

# Problem Links
- https://nados.io/question/abbreviation-1-using-bits
