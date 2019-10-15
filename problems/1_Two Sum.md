## 题目地址
https://leetcode.com/problems/two-sum/description/

## 题目描述
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 思路
构造一个字典，遍历时将(target - num)作为键，num的索引作为值存入字典。
同时遍历时都要判断当前num是否在字典中，在的话可以直接返回之前数的索引和当前数的索引。

## 代码
Python3:
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        num_dict = {}
        for i, num in enumerate(nums):
            if num in num_dict:
                return [num_dict[num], i]
            else:
                num_dict[target - num] = i
```

