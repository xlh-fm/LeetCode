## 题目地址
https://leetcode.com/problems/permutations/

## 题目描述
Given a collection of distinct integers, return all possible permutations.

Example:
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## 思路
1.对于输入列表，输出全排列的列表。  
2.使用回溯法，遍历数字，不在新列表里面的就放到最后，进入下一个回溯，回溯后移除最后一个数字。  
3.回溯法一开始进行判断，临时列表长度足够时，就加到全排列列表，注意要添加的是新的不受后面操作影响的列表，不能加引用，要加temp[:]。

## 代码
Python3:
```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:

        def backtrack(permutations, temp):
            if len(temp) == len(nums):
                permutations.append(temp[:])
            else:
                for num in nums:
                    if num in temp:
                        continue
                    temp.append(num)
                    backtrack(permutations, temp)
                    temp.pop()

        permutations = []
        backtrack(permutations, [])
        return permutations
```
