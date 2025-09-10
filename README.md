------------------------------------------------------
Week 4: Binary Search + Recursion
------------------------------------------------------
Day 22: Basic binary search (LC #704)
Day 23: First/last occurrence (LC #34)
Day 24: Search in rotated sorted array (LC #33)
Day 25: Square root via binary search (LC #69)
Day 26: Fibonacci recursion, climbing stairs (LC #509, #70)
Day 27: Subsets via recursion (LC #78)
Day 28: Practice binary search + recursion

"""
Day 22: Basic Binary Search (LC #704)
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Binary Search Basics
2. LeetCode #704 – Binary Search
"""

# ----------------------------------------------------
# 1. Binary Search Basics
# ----------------------------------------------------
"""
Binary Search works on sorted arrays.
Idea:
- Keep two pointers (left, right)
- Repeatedly check mid = (left + right) // 2
- If target == nums[mid] → return index
- If target < nums[mid] → search left half
- If target > nums[mid] → search right half

Time Complexity: O(log n)
Space Complexity: O(1)
"""


# ----------------------------------------------------
# 2. LeetCode #704 – Binary Search
# ----------------------------------------------------
"""
Problem:
Given an array of integers nums (sorted in ascending order)
and an integer target, return the index of target if found in nums.
If not, return -1.

Example:
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
"""

def search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1


# ----------------------------------------------------
# 3. Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [-1, 0, 3, 5, 9, 12]
    target = 9
    print("Input:", nums, "Target:", target)
    print("Output:", search(nums, target))  # Expected: 4

    target2 = 2
    print("Input:", nums, "Target:", target2)
    print("Output:", search(nums, target2))  # Expected: -1


# ----------------------------------------------------
# Time Complexity:
# - O(log n), where n = length of array
# Space Complexity:
# - O(1)
# ----------------------------------------------------
