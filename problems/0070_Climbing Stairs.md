## 题目地址
https://leetcode.com/problems/climbing-stairs/

## 题目描述
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## 思路
1.爬楼梯，每步爬1或2的阶梯，求爬到n一共有几种可能。  
2.用动态规划，爬1层有1种可能，2层有2种可能，因为每次爬1或2，所以接下来每层的可能都是前两层的可能之和。   
3.注意只有1层的情况。

## 代码
Python3:
```
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        dp = [0] * (n + 1)
        dp[1], dp[2] = 1, 2
        for i in range(3, n + 1):
            dp[i] = dp[i - 1] + dp[i - 2]
        return dp[n]
```
