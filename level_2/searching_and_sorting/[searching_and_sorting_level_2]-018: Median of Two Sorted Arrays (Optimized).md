# Problem Statement
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

[Tutorial](https://www.youtube.com/watch?v=jDJuW7tSxio&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=21)

# Thought Process
## Unoptimized
- Take two pointers at the beginning of both arrays, keep comparing and maintain a counter till we reach (n + m) / 2 in the counter

## Optimized
First we need to find a segregation:
- Do a binary search (or simply find the MID element) of first array
- We know that to find the correct segregation, total elements on left will be equal to (or one more) than the total on the right (as shown in the screenshot)

![image](https://user-images.githubusercontent.com/10897423/135707518-e743df49-1ea8-450b-a191-7c1dc7aa5f34.png)

- In the screenshot, we know there are 12 total elements (median will be at 6th place in the merged array), and first we checked segregation at a2. array b has 7 elements, so we will place the separator at `7 - 2 = 5` that is on the left of b5 or at b4.
- Now compare the validity of the segretator, and apply this again in left/right part of the array accordingly if condition is not satisfied
- Condition is: both elements on the left of segregator should be smaller than the right (here, a1 < b2 && b4 < a2)
- Condition not met, so we continue searching (notice lo, hi, mid in screenshot)

![image](https://user-images.githubusercontent.com/10897423/135707985-a4b45a6f-a83f-4528-9771-b86361196b44.png)


# Code
## Unoptimized
```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int l1 = 0, l2 = 0;
        int m = size(nums1), n = size(nums2);

        double med = 0, prev = 0;
        for(int k = 0; k < (n + m) / 2 + 1; ++k) {

            prev = med;

            if (l1 < m && l2 < n){
                med = nums1[l1] < nums2[l2] ? nums1[l1++] : nums2[l2++];
            } else {
                if (l1 < m) med = nums1[l1++];
                else med = nums2[l2++];
            }
        }

        if((n + m) & 1) {
            return med;
        } else {
            return (med + prev) / 2;
        }
    }
};
```

```cpp

```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/median-of-two-sorted-arrays/ojquestion
- https://leetcode.com/problems/median-of-two-sorted-arrays/
