# Data Structure基础知识
1. 链表
2. 单向链表
3. 双向链表
4. Java中Linkedlist使用双向链表
5. Time Space
6. 使用：
1）单链表反转
2）快慢指针：中间值问题；单链表是否有环；环的初始位置
3）约瑟夫问题


# Questions
## [61. Rotate List](https://leetcode.com/problems/rotate-list/)
### Question
Given the head of a linked list, rotate the list to the right by k places.

 

Example 1:


Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
Example 2:


Input: head = [0,1,2], k = 4
Output: [2,0,1]
 

Constraints:

The number of nodes in the list is in the range [0, 500].
-100 <= Node.val <= 100
0 <= k <= 2 * 109

### Algorithm
1. Find the old tail and connect it with the head old_tail.next = head to close the ring. Compute the length of the list n at the same time.

2. Find the new tail, which is (n - k % n - 1)th node from the head and the new head, which is (n - k % n)th node.

3. Break the ring new_tail.next = None and return new_head.

### Answer
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not head:
            return None
        if not head.next:
            return head
        
        # close the linked list into the ring
        old_tail = head
        n = 1
        while old_tail.next:
            old_tail = old_tail.next
            n += 1
        old_tail.next = head
        
        # find new tail: (n - k % n - 1)th node
        # and new head: (n - k % n)th node
        new_tail = head
        for i in range(n - k % n - 1):
            new_tail = new_tail.next
        new_head = new_tail.next
        
        # break the ring
        new_tail.next = None
        
        return new_head
```
## [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
### Question
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 

Example 1:


Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
 

Constraints:

The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zeros.

### Algorithm
1. 高精度加法
2. 指针
3. special cases:
1) two numbers with different lengths
2) sum has more digits

### Solution
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        result = ListNode(0)
        result_tail = result
        carry = 0
        
        while l1 or l2 or carry:
            val1 = (l1.val if l1 else 0)
            val2 = (l2.val if l2 else 0)
            carry, out = divmod(val1+val2+carry, 10)
            
            result_tail.next = ListNode(out)
            result_tail = result_tail.next
            
            l1 = (l1.next if l1 else None)
            l2 = (l2.next if l2 else None)
            
        return result.next
```

## [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
### Question
Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.

 

Example 1:


Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
Example 2:

Input: l1 = [], l2 = []
Output: []
Example 3:

Input: l1 = [], l2 = [0]
Output: [0]
 

Constraints:

The number of nodes in both lists is in the range [0, 50].
-100 <= Node.val <= 100
Both l1 and l2 are sorted in non-decreasing order.

### Algorithm
1. Iteration
2. Recursion T: O(n)

### Solution
1. Iteration
```
class Solution:
    def mergeTwoLists(self, l1, l2):
        # maintain an unchanging reference to node ahead of the return node.
        prehead = ListNode(-1)

        prev = prehead
        while l1 and l2:
            if l1.val <= l2.val:
                prev.next = l1
                l1 = l1.next
            else:
                prev.next = l2
                l2 = l2.next            
            prev = prev.next

        # At least one of l1 and l2 can still have nodes at this point, so connect
        # the non-null list to the end of the merged list.
        prev.next = l1 if l1 is not None else l2

        return prehead.next
```
2. Recursion
```
class Solution:
    def mergeTwoLists(self, l1, l2):
        if l1 is None:
            return l2
        elif l2 is None:
            return l1
        elif l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```            

## [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
### Question
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

 

Example 1:

Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
Example 2:

Input: lists = []
Output: []
Example 3:

Input: lists = [[]]
Output: []

### Algorithm
1. PriorityQueue
2. Divide and Conquer
![image](https://user-images.githubusercontent.com/27000065/126914241-0a821aa9-218f-4367-b522-9c8d2d8eccb1.png)


### Solution 2
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        amount = len(lists)
        interval = 1
        while interval < amount:
            for i in range(0, amount - interval, interval * 2):
                lists[i] = self.merge2Lists(lists[i], lists[i + interval])
            interval *= 2
        return lists[0] if amount > 0 else None

    def merge2Lists(self, l1, l2):
        head = point = ListNode(0)
        while l1 and l2:
            if l1.val <= l2.val:
                
                point.next = l1
                l1 = l1.next
               
            else:
                
                point.next = l2
                l2 = l1
                l1 = point.next.next
                
            point = point.next
        if not l1:
            point.next = l2
        else: 
            point.next = l1
        return head.next


```

## [148. Sort List](https://leetcode.com/problems/sort-list/)
![image](https://user-images.githubusercontent.com/27000065/127257072-0baaaee9-5d1d-4612-9b55-561748b54359.png)


## [725. Split Linked List in Parts](https://leetcode.com/problems/split-linked-list-in-parts/)
### Question
Given the head of a singly linked list and an integer k, split the linked list into k consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return an array of the k parts.

 

Example 1:


Input: head = [1,2,3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but its string representation as a ListNode is [].
Example 2:


Input: head = [1,2,3,4,5,6,7,8,9,10], k = 3
Output: [[1,2,3,4],[5,6,7],[8,9,10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
 

Constraints:

The number of nodes in the list is in the range [0, 1000].
0 <= Node.val <= 1000
1 <= k <= 50

### Algorithm
1. Splited input list
2. create a new list

# Solution
1.
```class Solution:
    def splitListToParts(self, root: ListNode, k: int) -> List[ListNode]:
        cur = root 
        for N in range(1001):
            if not cur: break
            cur = cur.next
        width, remainder = divmod(N, k)
    
        ans = [None] * k
        prev, head = None, root
        for i in range(k):
            ans[i] = head
             for j in range(width + (i < remainder)):
                prev, head = head, head.next
                
            if prev: prev.next = None
        return ans
```
2.
```class Solution(object):
    def splitListToParts(self, root, k):
        cur = root
        for N in xrange(1001):
            if not cur: break
            cur = cur.next
        width, remainder = divmod(N, k)

        ans = []
        cur = root
        for i in xrange(k):
            head = write = ListNode(None)
            for j in xrange(width + (i < remainder)):
                write.next = write = ListNode(cur.val)
                if cur: cur = cur.next
            ans.append(head.next)
        return ans
```    
write.next = write = ListNode(cur.val)
等价于
write.next = ListNode(cur.val)
write = write.next
1 = 2 = 3 -> 1 = 3 2 = 1
           
      
