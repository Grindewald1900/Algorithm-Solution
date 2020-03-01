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

![alt][base64str]



[base64str]:data:image/png;base64,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


