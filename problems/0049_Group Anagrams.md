## 题目地址
https://leetcode.com/problems/group-anagrams/

## 题目描述
Given an array of strings, group anagrams together.

Example:
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

## 思路
1.考虑用字典，把字符串排序后当key，原来的值组成的列表当value。  
2.字符串排序后变成列表，列表可变，不能直接当字典的key，要重新转换成字符串或者tuple。  
3.使用字典的get方法，key不存在时用默认值[]，再加上新添加的值，这样子就省得判断key在不在字典中了。  
4.返回字典的值的集合，注意要转换成list。  

## 代码
Python3:
```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dic = {}
        for str in strs:
            sorted_str = ''.join(sorted(str))
            dic[sorted_str] = dic.get(sorted_str, []) + [str]
        return list(dic.values())
```
