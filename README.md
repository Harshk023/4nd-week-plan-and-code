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


"""
Day 23: First and Last Occurrence in Sorted Array (LC #34)
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Binary Search Variation – Lower Bound & Upper Bound
2. LeetCode #34 – Find First and Last Position of Element in Sorted Array
"""

# ----------------------------------------------------
# Problem Statement (LC #34)
# ----------------------------------------------------
"""
Given an array of integers nums sorted in non-decreasing order,
find the starting and ending position of a given target value.

If target is not found in the array, return [-1, -1].

Example:
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3, 4]

Approach:
- Use binary search twice:
  - First to find the leftmost (first occurrence)
  - Second to find the rightmost (last occurrence)
- If target not found → return [-1, -1]

Time Complexity: O(log n)
Space Complexity: O(1)
"""

def searchRange(nums, target):
    def findFirst(nums, target):
        left, right = 0, len(nums) - 1
        index = -1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] >= target:
                right = mid - 1
            else:
                left = mid + 1
            if nums[mid] == target:
                index = mid
        return index
    
    def findLast(nums, target):
        left, right = 0, len(nums) - 1
        index = -1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] <= target:
                left = mid + 1
            else:
                right = mid - 1
            if nums[mid] == target:
                index = mid
        return index
    
    return [findFirst(nums, target), findLast(nums, target)]


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [5,7,7,8,8,10]
    target = 8
    print("Input:", nums, "Target:", target)
    print("Output:", searchRange(nums, target))  # Expected: [3, 4]

    target2 = 6
    print("Input:", nums, "Target:", target2)
    print("Output:", searchRange(nums, target2))  # Expected: [-1, -1]


# ----------------------------------------------------
# Time Complexity:
# - O(log n) for each binary search
# - Overall O(log n)
# Space Complexity:
# - O(1)
# ----------------------------------------------------


"""
Day 24: Search in Rotated Sorted Array (LC #33)
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Binary Search in Rotated Arrays
2. LeetCode #33 – Search in Rotated Sorted Array
"""

# ----------------------------------------------------
# Problem Statement (LC #33)
# ----------------------------------------------------
"""
There is an integer array nums sorted in ascending order (with distinct values).
It was rotated at an unknown pivot.
Given the array and an integer target, return the index of target if it exists, else -1.

Example:
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Approach:
- Perform modified binary search.
- At each step, one half of the array is sorted.
- Check if target lies in that half; if yes → search there, else → search the other half.

Time Complexity: O(log n)
Space Complexity: O(1)
"""

def search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        
        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    return -1


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    nums = [4,5,6,7,0,1,2]
    target = 0
    print("Input:", nums, "Target:", target)
    print("Output:", search(nums, target))  # Expected: 4

    target2 = 3
    print("Input:", nums, "Target:", target2)
    print("Output:", search(nums, target2))  # Expected: -1


# ----------------------------------------------------
# Time Complexity:
# - O(log n), since each step halves the search space
# Space Complexity:
# - O(1)
# ----------------------------------------------------

"""
Day 25: Square Root via Binary Search (LC #69)
Author: [Your Name]
Date: [Today's Date]

Topics Covered:
1. Binary Search for numerical problems
2. LeetCode #69 – Sqrt(x)
"""

# ----------------------------------------------------
# Problem Statement (LC #69)
# ----------------------------------------------------
"""
Given a non-negative integer x, return the square root of x rounded down
to the nearest integer. The returned integer should be non-negative.

You must not use built-in functions like sqrt().

Example:
Input: x = 8
Output: 2
(Explanation: sqrt(8) = 2.82... , rounded down to 2)
"""

# ----------------------------------------------------
# Approach:
# ----------------------------------------------------
"""
- Use binary search between 0 and x.
- Check mid * mid:
    - If == x → return mid
    - If < x → move right (store mid as possible answer)
    - If > x → move left
- Continue until left > right.

Time Complexity: O(log x)
Space Complexity: O(1)
"""

def mySqrt(x):
    if x < 2:  # sqrt(0)=0, sqrt(1)=1
        return x
    
    left, right = 0, x
    ans = 0
    
    while left <= right:
        mid = (left + right) // 2
        if mid * mid == x:
            return mid
        elif mid * mid < x:
            ans = mid  # store floor value
            left = mid + 1
        else:
            right = mid - 1
    return ans


# ----------------------------------------------------
# Example Usage
# ----------------------------------------------------
if __name__ == "__main__":
    x1 = 8
    print("Input:", x1, "Output:", mySqrt(x1))  # Expected: 2
    
    x2 = 16
    print("Input:", x2, "Output:", mySqrt(x2))  # Expected: 4
    
    x3 = 1
    print("Input:", x3, "Output:", mySqrt(x3))  # Expected: 1


# ----------------------------------------------------
# Time Complexity:
# - O(log x), since search space is halved each step
# Space Complexity:
# - O(1)
# ----------------------------------------------------
