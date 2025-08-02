# Problem Statement
1. There are 3 towers. Tower 1 has n disks, where n is a positive number. Tower 2 and 3 are empty.
2. The disks are increasingly placed in terms of size such that the smallest disk is on top and largest disk is at bottom.
3. You are required to

    3.1. Print the instructions to move the disks.

    3.2. from tower 1 to tower 2 using tower 3

    3.3. following the rules

        3.3.1 move 1 disk at a time.

        3.3.2 never place a smaller disk under a larger disk.

        3.3.3 you can only move a disk at the top.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is.Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=QDBrZFROuA0&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=12)

# Thought Process
- Use faith strategy!!!
- Call to move from 1 -> 3 using 2 (dont worry about _how_)
- Print `1 -> 2` implying that you are moving from 1 to 2 (actually 3 to 2) in this step
- Call to move from 3 -> 2

# Code
```cpp
void toh(int n, int n1, int n2, int n3) {
    if (n <= 0) return;

    toh(n - 1, n1, n3, n2);
    cout << n << "[" << n1 << " -> " << n2 << "]\n";
    toh(n - 1, n3, n2, n1);
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/introduction-to-recursion/toh-official/ojquestion
