## 题目地址
https://leetcode.com/problems/unique-paths/

## 题目描述
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

Example 1:
```
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
```
Example 2:
```
Input: m = 7, n = 3
Output: 28
```

## 思路1
1.用数学公式计算，格子是(m,n)的话，可能性就是C(m+n-2,n-1)。  
2.利用C的计算公式，先约分，简化计算，自己公式写一下，可以得出下面的循环，每次循环既乘也除，可以防止某一项的计算结果过大导致最后结果出错。  

## 代码1
Python3:
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        if m == 1 or n == 1:
            return 1
        m -= 1
        n -= 1
        if m < n:
            m, n = n, m
        ans = 1
        for i in range(1, n + 1):
            ans = ans * (m + n + 1 - i) / i
        return int(ans)
```
## 思路2
1.使用动态规划，思路是到达每个格子的路径数为到它上方和左边格子路径数的和。  
2.最上面一行和最左边一列的路径都是1。  

## 代码2
Python3:
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1] * n for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[m - 1][n - 1]
```
