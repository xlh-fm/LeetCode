## 题目地址
https://leetcode.com/problems/spiral-matrix/

## 题目描述
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

Example 1:
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```
Example 2:
```
Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## 思路
1.要求用顺时针螺旋状顺序来输出矩阵中的数。  
2.模拟一下输出会发现每次一圈输出，分成4个方向，然后不停地往里面缩进。  
3.用4个数代表4条边当前要输出的x或者y坐标。  
4.每当输出完一条边后那个方向的x或者y坐标向内缩进1，如果两个x坐标或者两个y坐标大小逆转了，就跳出循环。

## 代码
Python3:
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix:
            return []
        ans = []
        m = len(matrix)
        n = len(matrix[0])
        x1 = 0
        y1 = n - 1
        x2 = m - 1
        y2 = 0
        while True:
            for j in range(y2, y1 + 1):
                ans.append(matrix[x1][j])
            x1 += 1
            if x1 > x2:
                break
            for i in range(x1, x2 + 1):
                ans.append(matrix[i][y1])
            y1 -= 1
            if y1 < y2:
                break
            for j in range(y1, y2 - 1, -1):
                ans.append(matrix[x2][j])
            x2 -= 1
            if x1 > x2:
                break
            for i in range(x2, x1 - 1, -1):
                ans.append(matrix[i][y2])
            y2 += 1
            if y1 < y2:
                break
        return ans
```
