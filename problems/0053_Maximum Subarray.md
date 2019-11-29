## 题目地址
https://leetcode.com/problems/maximum-subarray/

## 题目描述
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## 思路
1.遍历列表的话，对于每个遍历到的数，遍历到它时包含它的最大子列表，要么是它自己本身，要么是它加上前面一个数的最大子列表的和。  
2.考虑用动态规划，用一个数组，记录每个数遍历到它时包含它的最大子列表的和。  
3.最后返回动态规划数组中的最大值。  
4.也可以不用数组，只用一个变量来记录每个数之前那个数的最大子列表的和。这样遍历时每次循环要拿当前的最大值和总的最大值比一下。

## 代码
Python3:
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [0] * len(nums)
        dp[0] = nums[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i - 1] + nums[i], nums[i])
        return max(dp)
```
