## 题目地址
https://leetcode.com/problems/container-with-most-water/

## 题目描述
Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai).   
n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0).   
Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note:
```
You may not slant the container and n is at least 2.
```
Example:
```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

## 思路
1.计算结果大小取决于左右的距离和更矮的那根柱子。  
2.从两边，距离最大的开始往中间移动直到距离为0，每次计算大小并和之前最大值比较。  
3.每次移动更矮的柱子，因为只有移动更矮的，长方形面积才有可能变大。  

## 代码
Python3:
```
from typing import List


class Solution:
    def maxArea(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        max_area = 0
        while l < r:
            max_area = max(max_area, (r - l) * min(height[l], height[r]))
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return max_area
```
