## 题目地址
https://leetcode.com/problems/sort-colors/

## 题目描述
Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

Example:
```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```
Follow up:

A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
Could you come up with a one-pass algorithm using only constant space?

## 思路
1.题目说了有一种方法是先统计012的数量，再写进去，要遍历两遍。  
2.题目要求遍历一遍。  
3.设置3个索引对应012,01的索引从头到尾，2的索引从后往前，当2的索引小于1时结束循环。  
4.0索引之前的都会是0,1索引之前到0索引都会是1,2索引之后的都会是2。  
5.当1的索引碰到数字0时，把它和0的索引的数字交换，01索引各加1。  
6.当1的索引碰到数字1时，直接1的索引加1。  
7.当1的索引碰到数字2时，和2的索引的数字交换，2的索引减1，因为交换来的数不知是多少，还要重新确认。

## 代码
Python3:
```
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        c1, c2, c3 = 0, 0, len(nums) - 1
        while c2 <= c3:
            if nums[c2] == 0:
                nums[c1], nums[c2] = nums[c2], nums[c1]
                c1 += 1
                c2 += 1
            elif nums[c2] == 1:
                c2 += 1
            else:
                nums[c2], nums[c3] = nums[c3], nums[c2]
                c3 -= 1
```
