# Binary Tree

## Question

Given an **sorted** integer array - nums, and an integer - target.

Find **any/first/last** position of target in nums.

return **-1** if target does not exist.

## Performance

T(n) = T(n/2) + O(1) = **O(log n)**

Use the required **Time Complexity** to guess the Way to solve the problem.

## Type

* Binary Search on Index
  * OOXX: find the first/last position that meets the condition.
  * Half Half: cut off the part without the answer.
* Binary Search on Result
  * No array.
  * Find out the max or min that meets the specific condition.
  * e.g. 69.sqrt(x), 875.kokoEatingBananas

## Code

```java
// Binary Search: return the index of the Target or -1
int binarySearch(int[] nums, int target) {
    int start = 0;
    int end = nums.length - 1; // inclusive boundary
    
    // [start, end], the termination condition should be when the boundary is empty, which is when start == end + 1. 
    while (start <= end) {
        int mid = start + (end - start) / 2; // avoid overflow | biased to the left.
        if (nums[mid] == target) {
            return mid; // find the target
        } else if (nums[mid] < target) {
            start = mid + 1; // [start, end] is inclusive, and mid has been checked.
        } else if (target < nums[mid]) {
            end = mid - 1;
        }
    }
    // no target
    return -1;
}

// Binary Search: return the first position/left boundary of the Target or -1
int leftBound(int[] nums, int target) {
    int start = 0;
    int end = nums.length - 1;
    
    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            end = mid - 1; // narrow down the upper bound and keep searching
        } else if (target < nums[mid]) {
            end = mid - 1;
        } else if (nums[mid] < target) {
            start = mid + 1;
        }
    }
    
    // target might not exist.
    // because the termination condition is when start = end + 1, 
    // then start might be out of bound when target is greater than all the elements.
    if (start >= nums.length || nums[start] != target) {
        return -1;
    }
    return start;
}

// Binary Search: return the last position/right boundary of the Target or -1
int rightBound(int[] nums, int target) {
    int start = 0;
    int end = nums.length - 1;
    
    while (start <= end) {
        int mid = start + (end - start) / 2;
        if (nums[mid] == target) {
            start = mid + 1; // scale up the lower bound and keep searching
        } else if (target < nums[mid]) {
            end = mid - 1;
        } else if (nums[mid] < target) {
            start = mid + 1;
        }
    }
    
    // target might not exist.
    // because the termination condition is when start = end + 1 (end = start - 1),
    // the end might be out of bound when the target is smaller than all the elements.
    if (end < 0 || nums[end] != target) {
        return -1;
    }
    return end;
}
```

