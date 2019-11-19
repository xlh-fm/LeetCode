## 题目地址
https://leetcode.com/problems/search-in-rotated-sorted-array/

## 题目描述
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
Example 2:
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

## 思路
1.有序的列表被中间截开，后面一段放到前面，意味着前面一段都比后面一段大。  
2.用二分法，low和high分别是列表的最前和最后索引，如果mid的值等于目标，即可返回索引。  
3.判断mid究竟在前面那一段还是后面那一段。  
4.然后判断target在mid前还是后，调整high或low。  
5.没有的话返回-1。  

## 代码
Python3:
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        low, high = 0, len(nums) - 1

        while low <= high:
            mid = (low + high) // 2
            if nums[mid] == target:
                return mid

            if nums[mid] >= nums[low]:
                if nums[low] <= target <= nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] <= target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1
        return -1
```
