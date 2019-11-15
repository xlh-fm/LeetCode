## 题目地址
https://leetcode.com/problems/valid-parentheses/

## 题目描述
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example:
```
Input: "([)]"
Output: false
```

## 思路
1.就是搞个栈，左括号放进去，右括号的话弹栈，看对不对，不对直接返回false。  
2.循环结束看栈是否为空，空返回true。  
3.字典用右括号当键，左括号当值。  

## 代码
Python3:
```
class Solution:
    def isValid(self, s: str) -> bool:
        dicts = {')': '(', '}': '{', ']': '['}
        stack = []
        for c in s:
            if c in dicts:
                if len(stack) == 0 or stack.pop() != dicts[c]:
                    return False
            else:
                stack.append(c)
        return not stack
```
