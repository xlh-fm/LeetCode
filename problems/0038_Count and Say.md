## 题目地址
https://leetcode.com/problems/count-and-say/

## 题目描述
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

Example 1:
```
Input: 1
Output: "1"
```
Example 2:
```
Input: 4
Output: "1211"
```

## 思路
1.创建一个函数，通过规则，输入字符串并输出答案。  
2.初始'1'，调用n-1次。  
3.设定一个count，对于每个字符，若跟下一个字符一样count+1，不同的话返回值后面加上次数和字符，重置count。  
4.因为要跟下一个比，所以先在字符串最后加一个非数字字符，防止越界。  

## 代码
Python3:
```
class Solution:
    def countAndSay(self, n: int) -> str:
        def build(ans: str) -> str:
            res = ''
            ans += 's'
            count = 1
            for i in range(len(ans) - 1):
                if ans[i] == ans[i + 1]:
                    count += 1
                else:
                    res = res + str(count) + ans[i]
                    count = 1
            return res

        ans = '1'
        for _ in range(n - 1):
            ans = build(ans)
        return ans
```
