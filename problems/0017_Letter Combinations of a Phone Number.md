## 题目地址
https://leetcode.com/problems/letter-combinations-of-a-phone-number/

## 题目描述
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example:
```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
Note:
```
Although the above answer is in lexicographical order, your answer could be in any order you want.
```

## 思路
1.要注意参数为空字符串的情况。  
2.对每个数字，获取数字对应的字母串。  
3.对结果集合中已存在的结果，每个结果往后接字母串中每个字母，并存入新的集合。  
4.注意初始集合中有一个空字符串。

## 代码
Python3:
```
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        dicts = {'2': 'abc',
                 '3': 'def',
                 '4': 'ghi',
                 '5': 'jkl',
                 '6': 'mno',
                 '7': 'pqrs',
                 '8': 'tuv',
                 '9': 'wxyz'}
        if not digits:
            return []
        results = ['']
        for digit in digits:
            temp = []
            letters = dicts[digit]
            for result in results:
                for letter in letters:
                    temp.append(result + letter)
            results = temp

        return results
```
