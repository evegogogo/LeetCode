# 81. Search in Rotated Sorted Array II

## Question

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., `[0,0,1,2,2,5,6]` might become `[2,5,6,0,0,1,2]`).

You are given a target value to search. If found in the array return `true`, otherwise return `false`.

**Example 1:**

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

**Example 2:**

```
Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
```

## Ideas

Similar to 33. One difference: there're duplicates, so we need to remove duplicates. 

![81](https://github.com/evegogogo/LeetCode/blob/master/images/81.png)

## Highlights

**Move the index to skip the duplicates**

## Code

```java
// Source : https://leetcode.com/problems/search-in-rotated-sorted-array-ii/
// Author: Eve
// Date: 2020-07-19

class Solution {
    public boolean search(int[] nums, int target) {
        int n = nums.length;
        if (nums == null || n == 0) {
            return false;
        }
        int start = 0;
        int end = n - 1;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return true;
            }
            // if left part is sorted
            if (nums[start] < nums[mid]) {
                // if target is in the left part
                if (target < nums[mid] && target >= nums[start]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
                // if right part is sorted
            } else if (nums[start] > nums[mid]) {
                // if target is in the rotated part
                if (target > nums[mid] && target <= nums[end]) {
                    start = mid + 1;
                } else {
                    end = mid - 1;
                }
            } else {
            // duplicates, nums[mid] == nums[start]
            // we can move the start remove duplicates
            // thus in the worest case, we would have target: 2, and array like 11111111, then
            // the running time would be O(n)
            start++;
            }
        }
        return false;
    }
}
```

