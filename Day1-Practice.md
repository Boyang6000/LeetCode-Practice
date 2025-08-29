# 📝 LeetCode 学习日志 Day 1

<br>

## 704. 二分查找
- 题目链接：[LeetCode 704. Binary Search](https://leetcode.com/problems/binary-search/)
- 关键词：Binary Search  


<br>

## 💡 思路
运用二分查找(Binary Search)，在 **左闭右闭区间** `[left, right]` 内查找 target：  


<br>

## 💻 代码实现
```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2; // 避免溢出
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else {
                return mid;
            }
        }
        return -1;
    }
}
