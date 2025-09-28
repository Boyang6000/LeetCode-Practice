# 📝 LeetCode 学习日志 Day 28

<br>

## 455. 分发饼干 
- 题目链接：[**LeetCode 455. Assign Cookies**](https://leetcode.com/problems/assign-cookies/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题采用了贪心算法，可以考虑大饼干先满足大胃口，或者小饼干先满足小胃口。


<br>

## 💻 代码实现
```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        if(g.length == 0 || s.length == 0) return 0;
        Arrays.sort(g);
        Arrays.sort(s);
        int count = 0;
        int index = s.length - 1;
        for(int i = g.length - 1; i >= 0; i--){
            if(index >= 0 && g[i] <= s[index]){
                count++;
                index--;
            }
        }
        return count;
    }
}
```

<br>

## 376. 摆动序列
- 题目链接：[**LeetCode 376. Wiggle Subsequence**](https://leetcode.com/problems/wiggle-subsequence/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题采用的是贪心算法，直接去看这个数字前后的差值。


<br>

## 💻 代码实现
```java
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if(nums.length <= 1) return nums.length;
        int curdiff = 0;
        int prediff = 0;
        int count = 1;
        for(int i = 1; i < nums.length; i++){
            curdiff = nums[i] - nums[i - 1];
            if((curdiff > 0 && prediff <= 0 || (curdiff < 0 && prediff >= 0))){
                count++;
                prediff = curdiff;
            }
        }
        return count;
    }
}
```

<br>

## 53. 最大子序和
- 题目链接：[**LeetCode 53. Maximum Subarray**](https://leetcode.com/problems/maximum-subarray/)
- 关键词：**Greedy**

<br>

## 💡 思路
这题贪心算法的思路在于，当当前subarray的sum小于等于0时，放弃当前array，转向下一个index开始进行计算。

<br>

## 💻 代码实现
```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums.length == 1) return nums[0];
        int sum = Integer.MIN_VALUE;
        int count =  0;
        for(int i = 0; i < nums.length; i++){
            count += nums[i];
            sum = Math.max(sum, count);
            if(count <= 0) count = 0;
       }
       return sum;
    }
}
```

<br>

## 📝 今日心得
今天是对于贪心算法的一个介绍，有的题目的贪心算法就比较简单，有的就比较复杂，总体来讲就是看怎么能节省步骤，就是贪心的本质。