# Problem Statement
1. A Professor conducts a Computer Science paper for N students. He had strictly instructed all students to sit according to their roll numbers. However when he started checking the papers, he found out that all the papers were randomly ordered because the students had sat randomly during the exam instead of sitting according to their roll numbers. The order is given in list of integers roll[ ]. The professor became very angry and he wanted to teach the students a lesson.
2. He decided to sort the papers according to roll numbers by Bubble Sort and count the number of swaps required for each and every student and deduct as many marks of a student as were the number of swaps required for that student. The marks of every student is given in list of integers marks[ ] in the order in which they were sitting. However he also has to maintain the class average greater than or equal to a set minimum avg, else he may lose his job.
3. The Professor wants to know whether he should punish the students or save his job.

[Tutorial](https://www.youtube.com/watch?v=VCA1_JapxqE&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=38)

# Thought Process
- Just count the total number of swaps to sort by bubble sort

# Code
```cpp
void solve(vector<int> roll, vector<int> marks, int n, int minAvg) {
    int swaps = 0;

    for (int itr = 1; itr < n; ++itr) {
        for (int i = 0; i < n - itr; ++i) {
            if (roll[i] > roll[i + 1]) {
                swaps += 2;             // Not ++, because we count both students separately
                swap(roll[i], roll[i + 1]);
            }
        }
    }

    int totalMarks = accumulate(marks.begin(), marks.end(), 0);
    int newMarks = totalMarks - swaps;
    double newAvg = double(newMarks - swaps) / n;

    cout << ((newAvg >= minAvg) ? "true\n" : "false\n");
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/punish-the-students-official/ojquestion
