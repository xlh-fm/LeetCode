## 题目地址
https://leetcode.com/problems/merge-k-sorted-lists/

## 题目描述
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:
```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

## 思路1
1.使用优先级队列，将所有数都放入队列中，优先级队列自动将小的数放在队列前面。  
2.依次取出数并且生成新的节点，全部连起来。  
3.返回头节点。  

## 代码1
Python3:
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

from queue import PriorityQueue

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        q = PriorityQueue()
        dummy = head = ListNode(0)
        for node in lists:
            while node:
                q.put(node.val)
                node = node.next
        while not q.empty():
            dummy.next = ListNode(q.get())
            dummy = dummy.next
            
        return head.next
```
## 思路2
1.动态规划，先实现两个链表的合并。  
2.k个链表的合并，可以看作是0~k/2列表中的链表和k/2~k个列表中的链表合并，  
也就是可以把列表一分为二，子列表，递归调用k的方法，返回值调用2的方法。  
3.递归结束的条件有列表长度为0,1,2三种。  

## 代码2
Python3:
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if not l1:
            return l2
        if not l2:
            return l1
        if l1.val <= l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2

    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if len(lists) == 0:
            return None
        if len(lists) == 1:
            return lists[0]
        if len(lists) == 2:
            return self.mergeTwoLists(lists[0], lists[1])
        l1 = lists[:len(lists) // 2]
        l2 = lists[len(lists) // 2:]

        return self.mergeTwoLists(self.mergeKLists(l1), self.mergeKLists(l2))
```
