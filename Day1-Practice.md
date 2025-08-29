# 📝 LeetCode 学习日志 Day 1



##  704. 二分查找
- 题目链接：[LeetCode 704. Binary Search](https://leetcode.com/problems/binary-search/)
- 关键词：Binary Search
---

## 💡 思路
运用Binary Search，在左闭右闭的范围里，通过缩小左右之间的范围来确定target的位置

## 💻 代码实现
```java
class Soluition{
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while(left <= right){
            int middle = (left + right) / 2;
            if(nums[middle] > target){
                right = middle - 1;
            }
            else if(nums[middle] < target){
                left = middle + 1;
            }
            else{
                return middle;
            }
        }

        return -1;
    }
}
```