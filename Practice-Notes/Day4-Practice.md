# 📝 LeetCode 学习日志 Day 4

<br>

## 24. 两两交换链表中的节点
- 题目链接：[**LeetCode 24. Swap Nodes in Pairs**](https://leetcode.com/problems/swap-nodes-in-pairs/)
- 关键词：**Linked List, Two Pointers**  

<br>

## 💡 思路
这道题的思路跟LeetCode 206 Reverse Linked List是一样的。**先加入一个dummy node 方便操作**，然后将dummy node，firstNode，secondNode，三个看作一个整体进行操作。剩余步骤同206。

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode temp, firstNode, secondNode;
        ListNode curNode = dummy;
        while(curNode.next != null && curNode.next.next != null){
            temp = curNode.next.next.next;
            firstNode = curNode.next;
            secondNode = curNode.next.next;
            curNode.next = secondNode;
            secondNode.next = firstNode;
            firstNode.next = temp;
            curNode = firstNode;
        }

        return dummy.next;
    }
}
```

<br>

##  19. 删除链表的倒数第N个节点
- 题目链接：[**LeetCode 19. Remove Nth Node From End of List**](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路
这道题第一次运用了快慢指针的思路，这个思路在linked list里面比较常见。首先加入**dummy node**， 将快慢指针同时指向dummy node，然后将快指针先移动n次，再同时移动快慢指针，当快指针到队尾时停下，此时慢指针正好指向要删除node前的一个node。

<br>

## 💻 代码实现
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;
        for(int i = 0; i < n; i++){
            fast = fast.next;
        }

        while(fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;
        return dummy.next;
    }
}
```

<br>

##  160. 链表相交
- 题目链接：[**LeetCode 160. Intersection of Two Linked Lists**](https://leetcode.com/problems/intersection-of-two-linked-lists/)
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路  
这道题的思路非常巧妙，将两个指针分别设置于两个链表的head，然后同时移动，当一个指针走到链表的结尾时，让他重新回到另一个链表的head，这样将两个链表链接起来，两个指针第二次经过相交点的路程就是一样的了。

<br>

## 💻 代码实现
```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA;
        ListNode p2 = headB;

        while(p1 != p2){
            p1 = p1 == null ? headB : p1.next;
            p2 = p2 == null ? headA : p2.next;
        }

        return p1;
    }
}
```

<br>

## 📝 今日心得
作为Day 1的题目，这三道题目都是比较基础的，其中Binary Search和Two Pointers这两个思想都是运用比较广泛的，这几道题目也是自己练过很多遍的，基本不会出现问题。希望能将这两个思路继续运用到别的不同的题目上面去
