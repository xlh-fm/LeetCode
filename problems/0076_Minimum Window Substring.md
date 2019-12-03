## 题目地址
https://leetcode.com/problems/minimum-window-substring/

## 题目描述
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

Example:
```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```
Note:

If there is no such window in S that covers all characters in T, return the empty string "".
If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

## 思路
1.题目要求找到包含所有T的字母的子串。  
2.用一个字典记录t中的元素和每个元素的个数，用begin和end两个指针选定窗口，用一个计数器记录窗口中t元素的个数。  
3.用end指针去探索，当begin到end-1之间的窗口满足条件时，再让begin往前移动，直到不再满足条件，  
这个过程中可以得到这次end对应最短的窗口，接下来让end继续往前跑。  
4.找到比之前更短的子串时候就用head表示开头，并记录新的最短窗口长度。  

## 代码
Python3:
```
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        counter, begin, end, head, length = 0, 0, 0, 0, len(s) + 1
        dic = collections.Counter(t)  # 生成键为t的元素，值为元素个数的字典
        while end < len(s):
            if s[end] in dic:  # 如果在t中
                dic[s[end]] -= 1
                if dic[s[end]] >= 0:
                    counter += 1
            end += 1  # 往后延伸
            while counter == len(t):  # 当前begin到end-1的子串符合要求
                if end - begin < length:  # 如果更短更新子串
                    head = begin
                    length = end - begin
                if s[begin] in dic:  # 如果在t中
                    dic[s[begin]] += 1
                    if dic[s[begin]] > 0:
                        counter -= 1  # 不再符合要求
                begin += 1
        return '' if length == len(s) + 1 else s[head:head + length]
```
