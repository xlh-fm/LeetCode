## 题目地址
https://leetcode.com/problems/merge-intervals/

## 题目描述
Given a collection of intervals, merge all overlapping intervals.

Example 1:
```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```
Example 2:
```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

## 思路
1.通过每个区间的第一个元素先进行排序，然后创建一个新列表等着插入区间。  
2.遍历原来的列表，注意如果新列表为空插入区间。  
3.如果新区间的起点大于新列表最后元素的终点，把新区间插入。  
4.否则的话，就是有重合的地方，因为新区间起点肯定大于等于最后元素的起点，所以这两个区间终点更大的就是合并区间的终点。

## 代码
Python3:
```
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort(key=lambda x: x[0])
        merged = []
        for interval in intervals:
            if not merged or interval[0] > merged[-1][1]:
                merged.append(interval)
            else:
                merged[-1][1] = max(merged[-1][1], interval[1])
        return merged
```
