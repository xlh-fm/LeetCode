## 题目地址
https://leetcode.com/problems/regular-expression-matching/

## 题目描述
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.
```
The matching should cover the entire input string (not partial).

Note:
```
s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or *.
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
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```
Example 3:
```
Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```
Example 4:
```
Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
```
Example 5:
```
Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```


## 思路1
1.使用递归。  
2.从前往后，每次用子串进行新的递归。  
3.每次递归先判断正则表达式是否为空，是的话返回字符串是否为空就是结果。  
4.判断字符串和正则表达式的第一个字符是否匹配。  
5.接下来，如果正则表达式第2个字符是\*，就有两种可能匹配成功，  
一种是这个\*什么都不匹配，当前匹配结果相当于字符串和跳过两个字符的正则表达式的匹配结果，  
一种是这个\*和字符串第一个字符匹配成功，因为\*可以匹配任意多的字符，所以在不知道字符串的情况下，  
只把字符串后移一位的子串与正则表达式继续匹配。  
6.如果正则表达式第2个字符不是\*，并且之前第一个字符匹配成功，  
字符串和正则表达式各后移一个字符继续匹配。  

## 代码1
Python3:
```
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        if not p:
            return not s
        first_match = len(s) > 0 and p[0] in [s[0], '.']

        if len(p) >= 2 and p[1] == '*':
            return self.isMatch(s, p[2:]) or first_match and self.isMatch(s[1:], p)
        else:
            return first_match and self.isMatch(s[1:], p[1:])
```

