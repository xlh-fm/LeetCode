## 题目地址
https://leetcode.com/problems/sqrtx/

## 题目描述
Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

Example 1:
```
Input: 4
Output: 2
```
Example 2:
```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```

## 思路
1.寻找正整数平方根。  
2.就用二分查找法寻找，如果mid的平方小于等于x，而(mid+1)的平方大于x，则可以返回mid。    

## 代码
Python3:
```
class Solution:
    def mySqrt(self, x: int) -> int:
        low, high = 0, x
        while low <= high:
            mid = (low + high) // 2
            if mid * mid <= x < (mid + 1) * (mid + 1):
                return mid
            if mid * mid < x:
                low = mid + 1
            else:
                high = mid - 1
```
