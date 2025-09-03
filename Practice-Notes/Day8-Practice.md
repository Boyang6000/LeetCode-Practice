# 📝 LeetCode 学习日志 Day 8

<br>

## 344. 反转字符串
- 题目链接：[**LeetCode 344. Reverse String**](https://leetcode.com/problems/reverse-string/)
- 关键词：**String**  

<br>

## 💡 思路
这个就是最基础的swap的运用，设定一个temp来储存值，然后将左边的值放到temp里面，再把右边的值赋给左边，最后把temp的值赋给右边就行

<br>

## 💻 代码实现
```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;

        while(left < right){
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```

<br>

## 541. 反转字符串 II
- 题目链接：[**LeetCode 541. Reverse String II**](https://leetcode.com/problems/reverse-string-ii/)
- 关键词：**String**

<br>

## 💡 思路
本题在344的基础上做了一些变动，核心方法还是swap的运用。首先，在Java里，**String 是不可变的**，所以我们得先把它变成char[], 或者可以使用StringBuilder来实现。我们这里选择的是用char[]，然后这道题是以2k长度为一个整体，那left每次开始就要加2k，right的值根据left走，或者整体长度不足k时right为最后一个数字，根据这个left和right来进行swap。最后将char[]重新变成string就行。

<br>

## 💻 代码实现
```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] arr = s.toCharArray();
        for(int i = 0; i < s.length(); i+=2*k){
            int left = i;
            int right = Math.min(i+k-1, arr.length - 1);
            while(left < right){
                char temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
                left++;
                right--;
            }
        }

        return new String(arr);
    }
}
```

<br>

## 📝 今日心得
今天的这两道题就比较基础，都是运用到了swap来做字符串反转，像第二题的话就要注意边界值，多思考思考for loop里每一次index增加的量，不用一定要是i++，也可以是别的increment。