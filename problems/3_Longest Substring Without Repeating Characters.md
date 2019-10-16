## 题目地址
https://leetcode.com/problems/longest-substring-without-repeating-characters/

## 题目描述
Given a string, find the length of the longest substring without repeating characters.

Example 1:
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```
Example 2:
```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
Example 3:
```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## 思路
1.创建一个空子串，用来按序存放每次循环到的字符。  
2.循环字符串，对每个字符，如果子串中不存在，就直接加进去。   
3.如果存在，将子串缩短成从存在字符后一位开始，再加入字符。
4.比较新子串长度和原来最大值。  
5.循环结束后返回最大值。    

## 代码
Python3:
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        longest = 0
        sub_str = []
        for c in s:
            if c in sub_str:
                sub_str = sub_str[sub_str.index(c) + 1:]
                sub_str.append(c)
            else:
                sub_str.append(c)
            longest = max(longest, len(sub_str))
        return longest
```
