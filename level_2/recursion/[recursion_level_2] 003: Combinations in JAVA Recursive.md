# Problem Statement

1. You are give a number of boxes (nboxes) and number of identical items (ritems).
2. You are required to place the items in those boxes and print all such configurations possible.

Items are identical and all of them are named 'i'.

Note 1 -> Number of boxes is greater than number of items, hence some of the boxes may remain 
                   empty.

Note 2 -> Check out the question video and write the recursive code as it is intended without 
                   changing signature. The judge can't force you but intends you to teach a concept.

[Tutorial](https://www.youtube.com/watch?v=wOaxJAtJ2Mo&list=PL-Jc9J83PIiHO9SQ6lxGuDsZNt2mkHEn0&index=4)

# Thought Process
- Each cell has 2 choices -> to place an item or to not place an item
- WE WILL NOT USE A FOR LOOP, REMEMBER
- For the first cell, we can `either place or not place` -> and find answer for the remaining boxes (currentBox++, filledBoxes++) or (currentBox++, filledBoxes)
- When we reach the n'th cell, if filledBoxes==r, we can print that arrangement, or else, do nothing

# Code

Implementation differs from tutorial but idea is same

```cpp
void combinations(string& boxes, int n, int r, int filledBoxes, int currentBox) {

    if (currentBox == n) {
        if (filledBoxes == r) {
            cout << boxes << "\n";
        }
        return;
    }

    boxes[currentBox] = 'i';
    combinations(boxes, n, r, filledBoxes + 1, currentBox + 1);
    boxes[currentBox] = '-';
    combinations(boxes, n, r, filledBoxes, currentBox + 1);
}

void solve(int n, int r) {
    string boxes(n, '-');
    combinations(boxes, n, r, 0, 0);
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/recursion-and-backtracking/combinations-i-official/ojquestion#!
