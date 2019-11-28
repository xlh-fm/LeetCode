## 题目地址
https://leetcode.com/problems/wildcard-matching/

## 题目描述
Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*'.
```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
```
The matching should cover the entire input string (not partial).

Note:
```
s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like ? or *.
```
Example 1:
```
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```
Example 2:
```
Input:
s = "aa"
p = "*"
Output: true
Explanation: '*' matches any sequence.
```
Example 3:
```
Input:
s = "cb"
p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```
Example 4:
```
Input:
s = "adceb"
p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```
Example 5:
```
Input:
s = "acdcb"
p = "a*c?b"
Output: false
```


## 思路
1.题目要求通配符匹配，使用动态规划，创建m+1,n+1的二维数组，因为有长度为0的情况。  
2.dp\[0]\[0]的时候为真。  
3.先处理一种特殊情况，当m为0时，因为连续的星号也能匹配空字符串，当第i个字符为星号时，它跟前一个结果一样。  
4.处理1到m个字符，和1到n个匹配模式字符的二层循环。  
5.如果匹配模式字符的第j个是星号，那么只要i,j-1为真，或者i-1，j为真，就为真，因为星号可以匹配空，也可以匹配任意多的字符。   
6.否则的话，就看第i个字符和第j个通配符是否匹配，并且结果还跟i-1，j-1有关。  
7.最后返回dp\[m]\[n]。  

## 代码
Python3:
```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        m = len(s)
        n = len(p)
        dp = [[False] * (n + 1) for _ in range(m + 1)]
        dp[0][0] = True
        for i in range(1, n + 1):
            if p[i - 1] == '*':
                dp[0][i] = dp[0][i - 1]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                if p[j - 1] == '*':
                    dp[i][j] = dp[i - 1][j] or dp[i][j - 1]
                else:
                    dp[i][j] = p[j - 1] in [s[i - 1], '?'] and dp[i - 1][j - 1]
        return dp[m][n]
```
