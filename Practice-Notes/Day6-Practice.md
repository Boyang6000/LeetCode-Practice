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

##  202. 快乐数
- 题目链接：[**LeetCode 202. Happy Number**](https://leetcode.com/problems/happy-number/)
- 关键词：**HashSet**

<br>

## 💡 思路  
这道题先要去理解什么情况下是happy number什么情况下不是。当运算结果等于1的时候就是happy number，如果运算过程中出现了重复结果就不是。储存每次结果跟重复挂钩时优先考虑HashSet。

这道题分为两步：
- 先写一个method来运算happy。先算这个数字mod10剩下的余数，就是最右边的这个digit。然后平方再加入到sum里面去，最后将这个数字除以10，就进入到下一个digit的运算。重复循环直至所有digit的平方都加入到了sum里面。
- 主要的method来看这个数字是否是happy number。先创建一个HashSet来储存所有出现的结果。当这个数字不等于1或者没有出现在HashSet里面时，将他加入到HashSet里，然后再进行happy运算，重复这个过程。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> check = new HashSet<>();
        while(n != 1 && !(check.contains(n))){
            check.add(n);
            n = happy(n);
        }

        return n == 1;
    }

    public int happy(int n){
        int sum = 0;
        while(n > 0){
            int digit = n % 10;
            sum += digit * digit;
            n = n / 10;
        }
        return sum;
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