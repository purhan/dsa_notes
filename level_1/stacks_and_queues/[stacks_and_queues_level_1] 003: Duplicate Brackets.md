# Problem Statement
1. You are given a string exp representing an expression.
2. Assume that the expression is balanced  i.e. the opening and closing brackets match with each other.
3. But, some of the pair of brackets maybe extra/needless.
4. You are required to print true if you detect extra brackets and false otherwise.

e.g.'
((a + b) + (c + d)) -> false
(a + b) + ((c + d)) -> true

[Tutorial](https://www.youtube.com/watch?v=aMPXhEdpXFA&list=PL-Jc9J83PIiEyUGT3S8zPdTMYojwZPLUM&index=3)

# Thought Process
- Create a stack `st`
- Traverse through the string, keep filling the array untill you find a `)`
- When you find a `)`, keep popping the stack untill you find and pop an `(`
- If you didn't need to pop anything (i.e. you found `(` right in the beginning) that means we had a duplicate pair of brackets

# Code
```cpp
void solve(string str) {
    stack<char> st;
    for (int i = 0; i < (int)str.length(); ++i) {
        char ch = str[i];
        if (ch != ')') {
            st.push(ch);
        } else {
            if (st.top() == '(') {
                cout << "true\n";
                return;
            }

            while (st.top() != '(') {
                st.pop();
            }
            st.pop();
        }
    }
    cout << "false\n";
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/stacks-and-queues/duplicate-brackets-official/ojquestion
