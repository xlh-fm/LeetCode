## 题目地址
https://leetcode.com/problems/subsets/

## 题目描述
Given a set of distinct integers, nums, return all possible subsets (the power set).

Example:
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
Note:
The solution set must not contain duplicate subsets.

## 思路
1.对无重复列表求全部的子集。  
2.用回溯法，深度优先，每次进入回溯就把当前的存进去。    

## 附类似问题的模板方案
https://leetcode.com/problems/subsets/discuss/27281/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning)

## 代码
Python3:
```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        ans = list()

        def backtrack(subset, start):
            ans.append(subset[:])
            for i in range(start, n):
                subset.append(nums[i])
                backtrack(subset, i + 1)
                subset.pop()

        backtrack([], 0)
        return ans
```
