## 题目地址
https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## 题目描述
Given a linked list, remove the n-th node from the end of list and return its head.

Example:
```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```
Note:
```
Given n will always be valid.
```
Follow up:
```
Could you do this in one pass?
```
## 思路
1.要求一次遍历解决。  
2.在列表最前面创建一个头结点会比较方便，避免删除列表第一个结点时的特殊情况。  
3.用两个指针，一个先往前跑n+1的路，然后两个一起跑，直到第一个为空。  
4.这时候第二个指针正好在要删除的节点前面。  
5.最后返回头结点的next即可。  
6.循环条件不放心的地方可以用简单数据自己试一下。

## 代码
Python3:
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        first = dummy
        second = dummy
        for _ in range(n + 1):
            first = first.next
        while first:
            first = first.next
            second = second.next
        second.next = second.next.next
        return dummy.next
```
