# 234 - 回文链表

## 题目描述
![problem](images/234.png)

>O(n) 的时间和 O(1) 的额外空间

## 方法
1. 找到链表中点，将其一分为二；
2. 将后半部分反转；
3. 前半部分与反转后的后半部分逐一比较。
注意：链表为空或只有一个元素均为回文链表。

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head or not head.next:
            return True

        # 将链表平分为前半部分head和后半部分slow
        fast = slow = prev = head
        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next
        prev.next = None

        # 将后半部分反转反转后为tmp
        curr = slow
        if not curr.next:
            right = slow
        else:
            while curr.next:
                tmp = ListNode(curr.next.val)
                tmp.next = slow
                slow = tmp
                curr.next = curr.next.next
            right = tmp
        
        # 比较两截链表
        left = head
        while left:
            if left.val != right.val:
                return False
            left = left.next
            right = right.next
        return True
```
