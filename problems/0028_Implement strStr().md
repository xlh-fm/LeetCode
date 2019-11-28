## 题目地址
https://leetcode.com/problems/implement-strstr/

## 题目描述
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:
```
Input: haystack = "hello", needle = "ll"
Output: 2
```
Example 2:
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```
Clarification:
What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

## 思路1
1.要求找到第一个子列在的索引。  
2.从头到可容纳子串的索引进行查找匹配。  
3.j发现和i不同的数，就让i加1，把j指向的数赋给i。  

## 代码1
Python3:
```
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i:i + len(needle)] == needle:
                return i
        return -1
```
## 思路2
1.可以直接用index方法。  

## 代码2
Python3:
```
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle not in haystack:
            return -1
        return haystack.index(needle)
```
