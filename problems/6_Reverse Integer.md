## 题目地址
https://leetcode.com/problems/string-to-integer-atoi/

## 题目描述
Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:
```
Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers 
within the 32-bit signed integer range: [−231,  231 − 1]. 
If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
```
Example 1:
```
Input: "42"
Output: 42
```
Example 2:
```
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```
Example 3:
```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```
Example 4:
```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```
Example 5:
```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```


## 思路
1.注意空字符串。  
2.跳过最前面的空格。  
3.生成数字。
4.注意判断生成数的范围。

## 代码
Python3:
```
class Solution:
    def myAtoi(self, str: str) -> int:
        if len(str) < 1:
            return 0
        cur, sign = 0, 1
        num = 0
        for i in range(len(str)):
            if str[i] != ' ':
                cur = i
                break
        if str[cur] not in ['-', '+', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9']:
            return 0
        if str[cur] == '-':
            cur += 1
            sign = -1
        elif str[cur] == '+':
            cur += 1
        while cur < len(str) and '9' >= str[cur] >= '0':
            num = num * 10 + int(str[cur])
            cur += 1
        num = num * sign
        if num > pow(2, 31) - 1:
            return pow(2, 31) - 1
        if num < -pow(2, 31):
            return -pow(2, 31)
        return num
```
