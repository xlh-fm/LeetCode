## 题目地址
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

## 题目描述
Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

Example 1:
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```
Example 2:
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

## 思路1
1.要求找出某个数的开始和结束的索引。  
2.从最前面往后找到第一个为开始的索引，跳出循环。  
3.如果没找到，直接返回[-1,-1]。  
4.从最后往前找，找到的第一个是结束的索引，跳出循环。  

## 代码1
Python3:
```
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        starting, ending = -1, -1
        for i in range(len(nums)):
            if nums[i] == target:
                starting = i
                break
        if starting == -1:
            return [-1, -1]
        for i in range(len(nums) - 1, -1, -1):
            if nums[i] == target:
                ending = i
                break
        return [starting, ending]
```

## 思路2
1.用二分查找法两次，分别找到左端点和右端点。  
2.因为不是查某个数，而是某个数在最左边的位置，所以跟平常的二分查找法有点区别。  
3.如果target更大，low要变成mid+1，如果是小于等于的话，high变成mid，这样子可以一步步让low变成最左边的target。  
4.同样方法查找最右端。  

## 代码2
Python3:
```
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        low, high = 0, len(nums) - 1
        starting, ending = -1, -1
        if not nums:
            return [starting, ending]
        while low < high:
            mid = (low + high) // 2
            if nums[mid] < target:
                low = mid + 1
            else:
                high = mid
        if nums[low] != target:
            return [starting, ending]
        else:
            starting = low
        high = len(nums) - 1
        while low < high:
            mid = (low + high) // 2 + 1
            if nums[mid] > target:
                high = mid - 1
            else:
                low = mid
        ending = high
        return [starting, ending]
```
