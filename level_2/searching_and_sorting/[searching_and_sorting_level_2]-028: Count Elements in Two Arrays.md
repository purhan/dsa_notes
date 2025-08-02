# Problem Statement
Given two unsorted arrays arr1[] and arr2[]. They may contain duplicates. For each element in arr1[] count elements less than or equal to it in array arr2[].

[Tutorial](https://www.youtube.com/watch?v=qE3RvSwfT9I&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=28)

# Thought Process

## Unoptimized
- Sort array `b`
- Traverse on array `a` and binary search for the last occurence of that value on `b`

## Optimized
- Optimized approach uses a hashmap and a prefix-sum array

# Code

## Unoptimized
![image](https://user-images.githubusercontent.com/10897423/135762983-a96f9b9a-0ce1-4fa3-8ebe-0b728e0442d5.png)

## Optimized

![image](https://user-images.githubusercontent.com/10897423/135763239-5997b2e2-e861-4691-ba24-95bfc1ea8e90.png)


# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/counting-elements-in-two-arrays-official/ojquestion#!
