## 题目地址
https://leetcode.com/problems/first-missing-positive/

## 题目描述
Given an unsorted integer array, find the smallest missing positive integer.

Example 1:
```
Input: [1,2,0]
Output: 3
```
Example 2:
```
Input: [3,4,-1,1]
Output: 2
```
Example 3:
```
Input: [7,8,9,11,12]
Output: 1
```

## 思路
1.要求找出不在数组中的最小正整数。  
2.思路就是把所有大于0并小于等于数组长度的数x，放到x-1的位置上。  
3.先遍历数组，如果发现一个数x大于0并小于等于数组长度，并且x-1位置上的数不是x，将x与x-1位置上的数交换。  
4.使用while，保证每次新交换过来的数也满足上述条件。  
5.经过上面循环，大于0并小于等于数组长度的数x都在x-1的位置上了。  
6.接着重新遍历数组，一旦发现i位置上的数不是i+1，就返回i+1，如果都符合，说明数组的数正好是1-n，那就返回n+1。  
7.注意交换时nums\[nums\[i] - 1], nums\[i]的位置，搞错了会陷入死循环。

## 代码
Python3:
```
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        n = len(nums)
        for i in range(n):
            while n >= nums[i] > 0 and nums[nums[i] - 1] != nums[i]:
                # nums[i], nums[nums[i] - 1] = nums[nums[i] - 1], nums[i]
                nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]
        for i in range(n):
            if nums[i] != i + 1:
                return i + 1
        return n + 1
```
