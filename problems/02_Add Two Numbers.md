## 题目地址
https://leetcode.com/problems/add-two-numbers/

## 题目描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:
```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 思路
1.创建一个无关结果的头结点。  
2.设置进位变量，设置游标指向头结点。  
3.因为两个链表长度不一定相等，所以循环条件是其中一个的当前结点不为空。  
4.计算两结点加上进位的和，生成这一位的结点和进位。  
5.连接结点，移动游标，移动两条链表游标。  
6.循环后，如果进位不为0，要增加一个结点。  
7.返回头结点的下一个结点。  

## 代码
Python3:
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        new_header = ListNode(0)
        carry = 0
        cur = new_header
        while l1 or l2:
            var1 = l1.val if l1 else 0
            var2 = l2.val if l2 else 0
            sum = var1 + var2 + carry
            new_node = ListNode(sum % 10)
            carry = 1 if sum >= 10 else 0
            cur.next = new_node
            cur = cur.next

            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
        if carry > 0:
            cur.next = ListNode(carry)
        return new_header.next
```
