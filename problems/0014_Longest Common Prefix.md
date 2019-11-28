## 题目地址
https://leetcode.com/problems/longest-common-prefix/

## 题目描述
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
```
Example 2:
```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## 思路
两个循环，先遍历数组中第一个字符串，拿每个字符和其余字符串的相同位置字符比较，
当索引超过某个字符串长度，或者字符不一致时，返回前缀。如果一次成功循环下来，前缀就加上那个字符。

## 代码
Python3:
```
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ""
        prefix = ""
        for i in range(len(strs[0])):
            for j in range(1, len(strs)):
                if i > len(strs[j]) - 1 or strs[0][i] != strs[j][i]:
                    return prefix
            prefix += strs[0][i]
        return prefix
```
