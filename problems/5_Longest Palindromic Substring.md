## 题目地址
https://leetcode.com/problems/longest-palindromic-substring/

## 题目描述
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
Example 2:
```
Input: "cbbd"
Output: "bb"
```

## 思路
1.有bab和baab两种回文。  
2.循环字符串，对每个字符，从中间往两边扩散，寻找最大回文。  

## 代码
Python3:
```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if len(s) <= 1:
            return s
        start, max_len = 0, 1
        for i in range(len(s)):
            len1 = self.expandAroundCenter(s, i, i)
            len2 = self.expandAroundCenter(s, i, i + 1)
            length = max(len1, len2)
            if length > max_len:
                max_len = length
                start = i - (length - 1) // 2
        return s[start:start + max_len]

    def expandAroundCenter(self, s: str, left: int, right: int) -> int:
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return right - left - 1
```
