# 16. 3Sum Closest

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

 

**Example 1:**

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

 

**Constraints:**

- `3 <= nums.length <= 10^3`
- `-10^3 <= nums[i] <= 10^3`
- `-10^4 <= target <= 10^4`

## Ideas

Based on Two Sum, add 1 more loop. 

We can fix 1 element and use 2 pointers within the range between the element to the end to find out the closest sum to the target.

## Highlights

**Remember to sort when using two pointers**

**Be careful about the edge**

## Code

```java
// Source: https://leetcode.com/problems/3sum-closest/solution/
// Author: Eve
// Date: 2020-7-17
    
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int diff = Integer.MAX_VALUE;
        int res = 0;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (Math.abs(sum - target) < diff) {
                    res = sum;
                    diff = Math.abs(sum - target);
                }
                if (sum < target) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return res;
    }
}
```

