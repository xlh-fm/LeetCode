## 题目地址
https://leetcode.com/problems/jump-game/

## 题目描述
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

Example 1:
```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```
Example 2:
```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

## 思路
1.从起点开始看能不能跳到终点，每次跳的距离为小于等于nums[index]的值里选择。  
2.尝试从最后一个点往前推，每次往前找前一个可以跳到终点的位置，把这个位置设置为新终点。  
3.最后终点的输出值为0，则为可以从起点跳到终点。  
4.之所以这种方法可行，是因为每次找到的新终点，确实可以跳到旧终点，
另外，就算有一个点不经过新终点就能跳到旧终点，由于每次跳的距离为小于等于nums[index]的值里选择，那这个点也一定能到新终点。

## 代码
Python3:
```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        end = len(nums) - 1
        for i in range(len(nums) - 1, -1, -1):
            if nums[i] >= end - i:
                end = i
        return end == 0
```
