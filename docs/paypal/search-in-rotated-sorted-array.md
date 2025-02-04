---
sidebar_position: 28
tags: [paypal]
---

# Search in Rotated Sorted Array

### Problem Statement

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

[Leetcode Link](https://leetcode.com/problems/search-in-rotated-sorted-array/)

#### Example 1:

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

#### Example 2:

```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

#### Example 3:

```
Input: nums = [1], target = 0
Output: -1
```

#### Constraints:

- 1 <= nums.length <= 5000
- -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
- All values of nums are unique.
- nums is an ascending array that is possibly rotated.
- -10<sup>4</sup> <= target <= 10<sup>4</sup>

### Code

```jsx title="Python"
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
        
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            # Left position
            if nums[left] <= nums[mid]:
                # if target is between start & mid, make right to (mid -1)
                if nums[left] <= target <= nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1

            # Right position
            else:
                # if target is between mid & end, make start to (mid + 1)
                if nums[mid] <= target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
```

