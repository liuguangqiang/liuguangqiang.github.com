---
layout : post 
category : LeetCode
desc : ''
title : Reverse Linked List
subtitle : 翻转一个单链表
catalog: true
author: "Eric"
tags:
   - LeetCode
   - Java
   - Python
---


## Reverse Linked List

### 题目介绍
* https://leetcode.com/problems/reverse-linked-list/
* Given the head of a singly linked list, reverse the list, and return the reversed list.
* 给定一个单链列表的头，
* 翻转列表，然后返回翻转的列表。

![image](/img/leetcode/reverseLinkedList.jpeg)

## 思路一: 递归
* 假设整个单链表只有两个节点head和next;
* 如果要翻转整个单链表， 那么只需要把单链表中的两个节点交换位置就可以了;

### java
```java
public static ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    ListNode next = head.next;
    ListNode newHead = reverseList(next);
    next.next = head;
    head.next = null;
    return newHead;
}
```

### python
```python
class Solution(object):
    def reverseList(self, head):
        if head is None or head.next is None:
            return head

        next = head.next
        newHead = self.reverseList(next)
        next.next = head
        head.next = None
        return newHead
```


## 思路二
* 从head节点开始遍历；
* 定义一个pre节点，表示上一个节点，用作反转后的节点的next节点；

### java
```java
public ListNode reverse(ListNode head) {
    ListNode node = head;
    ListNode pre = null;
    while (node != null) {
        ListNode next = node.next;
        node.next = pre;
        pre = node;
        node = next;
    }

    return pre;
}
```
