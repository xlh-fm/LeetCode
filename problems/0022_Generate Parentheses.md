## 题目地址
https://leetcode.com/problems/generate-parentheses/

## 题目描述
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

Example:
```
For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## 思路1
1.生成所有长度为2n的可能，并专门用一个方法进行检验。  
2.生成可能的方法是使用递归，每次递归时，加入一个左括号，调用递归，之后弹栈，加入右括号，执行递归。  
3.这相当于每次递归时，同一个位置上既去递归放左括号的可能性，也去递归放了右括号的可能性。  

## 代码1
Python3:
```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:

        def valid(l: List[str]):
            x = 0
            for c in l:
                if c == '(':
                    x += 1
                else:
                    x -= 1
                if x < 0:
                    return False
            return x == 0

        def generate(l: List[str] = []):
            if len(l) == 2 * n:
                if valid(l):
                    result.append(''.join(l))
            else:
                l.append('(')
                generate(l)
                l.pop()
                l.append(')')
                generate(l)
                l.pop()

        result = []
        generate()

        return result
```
## 思路2
1.使用回溯法，只在满足条件时才添加括号，而当长度为2n时必为有效答案。  
2.当左括号小于n时可以增加左括号调用递归。  
3.当右括号小于左括号数量时可以增加右括号调用递归。  

## 代码2
Python3:
```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        result = []

        def backtrack(a='', l=0, r=0):
            if len(a) == 2 * n:
                result.append(a)
                return
            if l < n:
                backtrack(a + '(', l + 1, r)
            if r < l:
                backtrack(a + ')', l, r + 1)

        backtrack()
        return result
```
