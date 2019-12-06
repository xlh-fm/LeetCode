## 题目地址
https://leetcode.com/problems/word-search/

## 题目描述
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell,   
where "adjacent" cells are those horizontally or vertically neighboring.   
The same letter cell may not be used more than once.

Example:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

## 思路
1.使用深度优先来找路径。  
2.遍历矩阵中每个字母，以该字母为开头来进行查找。  
3.进入深度优先，若参数词长度为0，说明这个词已经全部找到，返回真。  
4.若i，j越界或当前字母不对应，返回假。  
5.从四个方向对这个词的word[1:]继续深度优先查找，在那之前，为了防止自己这个被访问过的又被访问，  
先改一下当前位置的值，获得返回值之后改回来。

## 代码
Python3:
```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        if not board:
            return False
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.dfs(board, i, j, word):
                    return True
        return False

    def dfs(self, board, i, j, word):
        if len(word) == 0:
            return True
        if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]) or word[0] != board[i][j]:
            return False
        temp = board[i][j]  # 已经访问过了，所以防止再被访问
        board[i][j] = ''
        ans = self.dfs(board, i + 1, j, word[1:]) or self.dfs(board, i - 1, j, word[1:]) or \
            self.dfs(board, i, j + 1, word[1:]) or self.dfs(board, i, j - 1, word[1:])
        board[i][j] = temp
        return ans
```
