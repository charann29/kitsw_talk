# LeetCode – Merge Sort Based Problems
**Date: December 17th**

## Problem List

### 1. Sort an Array
**Link:** https://leetcode.com/problems/sort-an-array/

Classic implementation of merge sort algorithm to sort an array in ascending order.

**Key Concepts:**
- Basic merge sort implementation
- Divide and conquer approach
- Time complexity: O(n log n)

---

### 2. Merge Sorted Array
**Link:** https://leetcode.com/problems/merge-sorted-array/

Merge two sorted arrays into one sorted array, with one array having enough space to hold both.

**Key Concepts:**
- Two-pointer technique
- In-place merging
- Working backwards to avoid overwriting

---

### 3. Merge Two Sorted Lists
**Link:** https://leetcode.com/problems/merge-two-sorted-lists/

Merge two sorted linked lists into one sorted linked list.

**Key Concepts:**
- Linked list manipulation
- Merge operation from merge sort
- Dummy node technique

---

### 4. Sort List
**Link:** https://leetcode.com/problems/sort-list/

Sort a linked list using merge sort algorithm.

**Key Concepts:**
- Merge sort on linked lists
- Finding middle of linked list (slow/fast pointers)
- Bottom-up or top-down approach

---

### 5. Count of Smaller Numbers After Self
**Link:** https://leetcode.com/problems/count-of-smaller-numbers-after-self/

Count how many numbers after each element are smaller than it.

**Key Concepts:**
- Modified merge sort with counting
- Index tracking during merge
- Inverse pairs counting

---

### 6. Reverse Pairs
**Link:** https://leetcode.com/problems/reverse-pairs/

Find the number of reverse pairs where i < j and nums[i] > 2 * nums[j].

**Key Concepts:**
- Enhanced merge sort
- Counting pairs during merge process
- Two-pointer technique for counting

---

### 7. Count of Range Sum
**Link:** https://leetcode.com/problems/count-of-range-sum/

Count the number of range sums that lie in a given range.

**Key Concepts:**
- Prefix sum + merge sort
- Counting valid ranges during merge
- Advanced merge sort application

---

### 8. Number of Pairs Satisfying Inequality
**Link:** https://leetcode.com/problems/number-of-pairs-satisfying-inequality/

Count pairs (i, j) where i < j and the given inequality is satisfied.

**Key Concepts:**
- Transform inequality to simpler form
- Merge sort with counting
- Similar to reverse pairs problem

---

### 9. Merge K Sorted Lists
**Link:** https://leetcode.com/problems/merge-k-sorted-lists/

Merge k sorted linked lists into one sorted list.

**Key Concepts:**
- Divide and conquer (pairwise merging)
- Min-heap approach (alternative solution)
- Time complexity: O(N log k) where N is total nodes

---

## Common Patterns

1. **Basic Merge Operation**: Problems 2, 3, 9 focus on the fundamental merge operation
2. **Counting During Merge**: Problems 5, 6, 7, 8 use merge sort to efficiently count inversions or pairs
3. **Sorting Complex Structures**: Problems 4, 9 apply merge sort to linked lists
4. **Modified Merge Sort**: Advanced problems require tracking additional information during the merge process

## Study Tips

- Master the basic merge sort algorithm first (Problem 1)
- Understand the merge operation thoroughly (Problems 2, 3)
- Practice counting techniques during merge (Problems 5, 6)
- Work on problems progressively from easy to hard
- Pay attention to space complexity optimizations
