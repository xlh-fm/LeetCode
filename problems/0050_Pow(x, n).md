## 题目地址
https://leetcode.com/problems/powx-n/

## 题目描述
Implement pow(x, n), which calculates x raised to the power n (xn).

Example1:
```
Input: 2.00000, 10
Output: 1024.00000
```
Example2:
```
Input: 2.10000, 3
Output: 9.26100
```
Example3:
```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

## 思路
1.n次方计算，如果n是负数的话，把x变成1/x，n变成-n即可。  
2.思路是在循环中，让n不停除于2，同时让x变成x*x。  
3.n为奇数时会余1，只是除于2会损失，要让答案在这时候乘上此时的x的值。  

## 代码
Python3:
```
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            x = 1 / x
            n = -n
        ans = 1
        while n:
            if n % 2 == 1:
                ans *= x
            x *= x
            n //= 2
        return ans
```
