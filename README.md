# GFG_27
---
Difficulty: Hard  
Source: 160 Days of Problem Solving  
Tags:
  - Sorting
  - Mathematical
---

# 🚀 _Day 27. Merge Without Extra Space_ 🧠


The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/sorting-gfg-160/problem/merge-two-sorted-arrays-1587115620)


## 💡 **Problem Description:**

Given two sorted arrays `a[]` and `b[]` in non-decreasing order, merge them in sorted order **without using any extra space**.  
Modify `a[]` to contain the first `n` smallest elements, and modify `b[]` to contain the remaining `m` elements in sorted order.  


## 🔍 **Example Walkthrough:**

**Input:**  
`a[] = [2, 4, 7, 10], b[] = [2, 3]`  
**Output:**  
`a[] = [2, 2, 3, 4]`  
`b[] = [7, 10]`  

**Explanation:**  
After merging, the sorted order is `[2, 2, 3, 4, 7, 10]`.  
The first `n` elements go into `a[]`, and the remaining elements go into `b[]`.

**Input:**  
`a[] = [1, 5, 9, 10, 15, 20], b[] = [2, 3, 8, 13]`  
**Output:**  
`a[] = [1, 2, 3, 5, 8, 9]`  
`b[] = [10, 13, 15, 20]`  

**Explanation:**  
After merging, the sorted order is `[1, 2, 3, 5, 8, 9, 10, 13, 15, 20]`.  

**Constraints:**  
- `1 <= a.size(), b.size() <= 10^5`  
- `0 <= a[i], b[i] <= 10^7`


## 🎯 **My Approach:**

This problem can be solved using the **Gap Algorithm**, which reduces the need for extra space while efficiently merging two sorted arrays.  

### Steps:  

1. **Calculate Initial Gap:**  
   - Combine the sizes of both arrays, `n + m`, and compute the initial gap as `(n + m) // 2 + (n + m) % 2`.

2. **Iterative Comparison:**  
   - Using the gap, compare elements in both arrays. Swap them if they are out of order.  
   - Reduce the gap in each iteration until it becomes `0`.

3. **Handle Overlapping Cases:**  
   - Handle cases where elements of `a[]` need to be swapped with `b[]`.

4. **Ensure Final Order:**  
   - After processing, the arrays will be modified in-place to reflect the merged sorted order.


## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O((n + m) * log(n + m))  
   - The gap reduces logarithmically with each iteration (`log(n + m)` iterations).  
   - Each iteration performs comparisons and swaps in O(n + m).  
   - Hence, the total complexity is O((n + m) * log(n + m)).  

- **Expected Auxiliary Space Complexity:** O(1)  
   - No extra space is used; modifications are done in-place.


## 📝 **Solution Code**
## Code (Python)

```python
class Solution:
    def nextGap(self, gap):
        return 0 if gap <= 1 else (gap // 2) + (gap % 2)

    def mergeArrays(self, a, b):
        n, m = len(a), len(b)
        gap = n + m

        while gap > 0:
            gap = self.nextGap(gap)
            i, j = 0, 0

            while i + gap < n:
                if a[i] > a[i + gap]:
                    a[i], a[i + gap] = a[i + gap], a[i]
                i += 1

            j = max(gap - n, 0)
            i = 0 if gap > n else n - gap
            while i < n and j < m:
                if a[i] > b[j]:
                    a[i], b[j] = b[j], a[i]
                i += 1
                j += 1
            j = 0
            while j + gap < m:
                if b[j] > b[j + gap]:
                    b[j], b[j + gap] = b[j + gap], b[j]
                j += 1
```
