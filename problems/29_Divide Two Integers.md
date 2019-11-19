## 题目地址
https://leetcode.com/problems/divide-two-integers/

## 题目描述
Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero.

Note:
```
Both dividend and divisor will be 32-bit signed integers.
The divisor will never be 0.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1].   
For the purpose of this problem, assume that your function returns 231 − 1 when the division result overflows.
```
Example 1:
```
Input: dividend = 10, divisor = 3
Output: 3
```
Example 2:
```
Input: dividend = 7, divisor = -3
Output: -2
```

## 思路
1.要求不能用乘除法和模来计算商。  
2.用绝对值计算会比较方便。  
3.用被除数一次一次减除数，计数也可以得到商，但是太慢了。  
4.在这里，每个循环内进行一个小循环，让除数叠加自己，相当于乘2的n次方，快速增加到比被除数大，同时临时的商也做相同运算。  
5.被除数减去叠加的除数，商加上这次循环的商。  

## 代码
Python3:
```
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        sign = -1
        quotient = 0
        if dividend >= 0 and divisor > 0 or dividend <= 0 and divisor < 0:
            sign = 1
        a = abs(dividend)
        b = abs(divisor)
        while a - b >= 0:
            c = b
            current_quotient = 1
            while c + c <= a:
                c += c
                current_quotient += current_quotient
            a -= c
            quotient += current_quotient
        if sign == 1:
            return min(quotient, pow(2, 31) - 1)
        else:
            return max(-quotient, -1 * pow(2, 31))
```
