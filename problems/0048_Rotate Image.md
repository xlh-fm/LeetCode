## 题目地址
https://leetcode.com/problems/rotate-image/

## 题目描述
You are given an n x n 2D matrix representing an image.
Rotate the image by 90 degrees (clockwise).

Note:
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly.  
DO NOT allocate another 2D matrix and do the rotation.

Example1:
```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

Example2:
```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

## 思路
1.题目要求对二维图像(n*n)顺时针转90度，并在原二维数组上操作。  
2.对于图上任何一个点(x,y)，顺时针转90度坐标就变成(y,n-1-x)。  
3.旋转一个点可以牵动到4个点，因此只需要遍历图的左上角即可。  
4.n为偶数时只要用n/2就可以处理，但是奇数时还多了一个十字(一行和一列)要处理，所以y in range(n - n // 2)。  

## 代码
Python3:
```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        for x in range(n // 2):
            for y in range(n - n // 2):
                matrix[x][y], matrix[y][n - 1 - x], matrix[n - 1 - x][n - 1 - y], matrix[n - 1 - y][x] = \
                    matrix[n - 1 - y][x], matrix[x][y], matrix[y][n - 1 - x], matrix[n - 1 - x][n - 1 - y]
```
