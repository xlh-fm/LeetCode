## 题目地址
https://leetcode.com/problems/reverse-integer/submissions/

## 题目描述
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:
```
Input: 123
Output: 321
```
Example 2:
```
Input: -123
Output: -321
```
Example 3:
```
Input: 120
Output: 21
```
Note:
```
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.
```

## 思路
1.对输入每次取10的余数，加到生成数的最后。  
2.Python负数取余得到的结果会与要求不一致，所以使用输入值的绝对值，负数的话最后取负数就行。  
3.最后判断生成数的范围。

## 代码
Python3:
```
class Solution:
    def reverse(self, x: int) -> int:
        y = 0
        z = abs(x)
        while z != 0:
            y = y * 10 + z % 10
            z = z // 10
        if (x < 0):
            y = -y
        if y > pow(2, 31) - 1 or y < -pow(2, 31):
            return 0
        return y
```
