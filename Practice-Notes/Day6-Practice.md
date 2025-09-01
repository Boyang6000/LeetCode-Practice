# 📝 LeetCode 学习日志 Day 4

<br>

## 242. 有效的字母异位词
- 题目链接：[**LeetCode 242. Valid Anagram**](https://leetcode.com/problems/valid-anagram/)
- 关键词：**HashTable**  

<br>

## 💡 思路
这道题因为长度的限制，所以可以使用list来代替hashmap。先创建一个int list来存放每个字母出现的次数，然后循环s来看每个字母出现多少次，出现一次就在int list相对应的位置加1。然后再看t每个字母出现多少次，出现一次就在int list相对应的位置减1。最后来看是否int list里面每个数字都是0，如果不是就return false。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] ans = new int[26];

        for(int i = 0; i < s.length(); i++){
            ans[s.charAt(i) - 'a']++;
        }

        for(int j = 0; j < t.length(); j++){
            ans[t.charAt(j) - 'a']--;
        }

        for(int k: ans){
            if(k != 0){
                return false;
            }
        }
        return true;
    }
}
```

<br>

##  349. 两个数组的交集
- 题目链接：[**LeetCode 349. Intersection of Two Arrays**](https://leetcode.com/problems/intersection-of-two-arrays/)
- 关键词：**HashSet**

<br>

## 💡 思路
因为HashSet不允许出现重复的值，重复的值添加进去将会被忽略，所以这里我们使用HashSet。先创建第一个HashSet，将nums1里面的数字都添加进去，然后再创建第二个HashSet，如果num2的数字出现在第一个HashSet里，将这个数字加入到第二个HashSet里面。这样既确保了这个数字同时出现在两个list里面，并且答案数字不会重复。最后将答案HashSet里面的数字转化成list。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> check = new HashSet<>();
        Set<Integer> ans = new HashSet<>();

        for(int i: nums1){
            check.add(i);
        }

        for(int j: nums2){
            if(check.contains(j)){
                ans.add(j);
            }
        }

        int[] result = new int[ans.size()];
        int count = 0;
        for(int i: ans){
            result[count] = i;
            count++;
        }

        return result;
    }
}
```

<br>

##  160. 链表相交
- 题目链接：[**LeetCode 160. Intersection of Two Linked Lists**](https://leetcode.com/problems/intersection-of-two-linked-lists/)
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路  
这道题的思路非常巧妙，第一次做的话基本上想不到，将两个指针分别设置于两个链表的head，然后同时移动，当一个指针走到链表的结尾时，让他重新回到另一个链表的head，这样将两个链表链接起来，两个指针第二次经过相交点的路程就是一样的了。

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

##  142. 环形链表II
- 题目链接：[**LeetCode 142. Linked List II**]（https://leetcode.com/problems/linked-list-cycle-ii/）
- 关键词：**Linked List, Two Pointers**

<br>

## 💡 思路  
这道题的思路非常巧妙，第一次做的话基本上想不到，也非常的反直觉。先将快慢指针同时指向head，然后快指针每次移动两个node，慢指针每次移动一个node。如果快指针到结尾都没跟慢指针相遇，说明没有loop。如果快慢指针相遇了，说明有loop，此时再设定一个指针在head，然后这个指针跟慢指针每次移动一个node，最终他们会相遇在loop的开始点。

<br>

## 💻 代码实现
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;

            if(fast == slow){
                ListNode target = head;
                while(target != slow){
                    target = target.next;
                    slow = slow.next;
                }
                return target;
            }
        }
        return null;
    }
}
```

<br>

## 📝 今日心得
今天的这四道题目相对而言是比较有难度的，如果是第一次做的话很难想到办法。其中160和142这两道比较的反直觉，需要做完多加深巩固印象，不是能靠暴力解决能实现的。在linked list里面比较重要的两点就是添加dummy node和使用快慢指针，会很方便。