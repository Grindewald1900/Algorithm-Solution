# 2. Add Two Numbers

## Description:

### You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

### You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

## Solution 1.0
Define two Int variables:  
count: the carry of two numbers  
sumDigit: the sum of two numbers and the count.
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode p = l1, q = l2, sum = result;
        int sumDigit = 0;
        int count = 0;
        int num1 = 0, num2 = 0;
        
        while(p != null || q != null){
            num1 = (null == p) ?  0 : p.val;
            num2 = (null == q) ?  0 : q.val;
            sumDigit = num1 + num2 + count;
            count = sumDigit/10;
            sum.next = new ListNode(sumDigit%10);
            if(null != p){
                p = p.next;
            }
            if(null != q){
                q = q.next;
            }
            sum = sum.next;
        }
        return result.next;
    }
}
```

1363 / 1563 test cases passed.
Status: Wrong Answer
Submitted: 3 minutes ago
Input:
[5]
[5]
Output:
[0]
Expected:
[0,1]



## Solution 1.1
The error detected by the test case is caused by not dealing with the carry for the last digit.
```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode result = new ListNode(0);
        ListNode p = l1, q = l2, sum = result;
        int sumDigit = 0;
        int count = 0;
        int num1 = 0, num2 = 0;
        
        while(p != null || q != null){
            num1 = (null == p) ?  0 : p.val;
            num2 = (null == q) ?  0 : q.val;
            sumDigit = num1 + num2 + count;
            count = sumDigit/10;
            sum.next = new ListNode(sumDigit%10);
            if(null != p){
                p = p.next;
            }
            if(null != q){
                q = q.next;
            }
            sum = sum.next;
        }
        if(count > 0){
            sum.next = new ListNode(1);
        }
        return result.next;
    }
}
```
Runtime: 2 ms, faster than 78.11% of Java online submissions for Add Two Numbers.
Memory Usage: 41 MB, less than 91.22% of Java online submissions for Add Two Numbers.  

## Something related
单向链表是一种线性表，实际上是由节点（Node）组成的，一个链表拥有不定数量的节点。其数据在内存中存储是不连续的，它存储的数据分散在内存中，每个结点只能也只有它能知道下一个结点的存储位置。由N各节点（Node）组成单向链表，每一个Node记录本Node的数据及下一个Node。向外暴露的只有一个头节点（Head），我们对链表的所有操作，都是直接或者间接地通过其头节点来进行的。

![avatar](https://img-blog.csdn.net/20160420141138723)  
每个节点包含本身数据及下一节点的引用

![avatar](https://img-blog.csdn.net/20160420134010570)

![avatar](https://img-blog.csdn.net/20160420134000174)


