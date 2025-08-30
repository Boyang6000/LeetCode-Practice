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

##  27. 移除元素
- 题目链接：[**LeetCode 27. Remove Element**](https://leetcode.com/problems/remove-element/)
- 关键词：**Two Pointers**

<br>

## 💡 思路
运用Two Pointers，一个指针记录当前的index，另一个指针记录不需要remove的数量，如果当前index不需要remove，就放在另一个指针的位置然后update  

<br>

## 💻 代码实现
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int count = 0;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != val){
                nums[count] = nums[i];
                count++;
            }
        }

        return count;
    }
}
```

<br>

##  977. 有序数组的平方
- 题目链接：[**LeetCode 977. Squares of a Sorted Array**](https://leetcode.com/problems/squares-of-a-sorted-array/)
- 关键词：**Two Pointers**

<br>

## 💡 思路  
先将所有的数字根据他们的绝对值大小进行排序，用两个指针分别指向left和right进行大小比较，将另一个指针放在新的Array的队尾，将大的数字放在另一个指针的位置，然后update所有指针的位置。当排序完成时，将每个数字平方即可

<br>

## 💻 代码实现
```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int index = nums.length - 1;
        int left = 0;
        int right = nums.length - 1;
        int[] ans = new int[nums.length];

        while(left <= right){
            if(Math.abs(nums[left]) > Math.abs(nums[right])){
                ans[index] = nums[left];
                index--;
                left++;
            }
            else{
                ans[index] = nums[right];
                index--;
                right--;
            }
        }

        for(int i = 0; i < ans.length; i++){
            ans[i] = ans[i] * ans[i];
        }

        return ans;
    }
}
```

<br>

## 📝 今日心得
作为Day 1的题目，这三道题目都是比较基础的，其中Binary Search和Two Pointers这两个思想都是运用比较广泛的，这几道题目也是自己练过很多遍的，基本不会出现问题。希望能将这两个思路继续运用到别的不同的题目上面去
