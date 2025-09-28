# 📝 LeetCode 学习日志 Day 29

<br>

## 134. 加油站
- 题目链接：[**LeetCode 134. Gas Station**](https://leetcode.com/problems/gas-station/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题采用了贪心算法,是一个非常巧妙的思路。首先很明显的就是，如果totalGas < totalCost的话，是肯定跑不完一圈的。

那重点就在于怎么去寻找可以跑完一圈的那个点。可以通过计算一段区间的totalSum，如果这个区间的totalSum < 0, 说明不是从里面的这个点开始的，那么start点就应该是 i + 1。


<br>

## 💻 代码实现
```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int curSum = 0;
        int totalSum = 0;
        int index = 0;
        for(int i = 0; i < gas.length; i++){
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if(curSum < 0){
                index = i + 1;
                curSum = 0;
            }
        }
        if(totalSum < 0) return -1;
        return index;
    }
}
```

<br>

## 55. 跳跃游戏
- 题目链接：[**LeetCode 55. Jump Game**](https://leetcode.com/problems/jump-game/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题采用的是贪心算法，计算跳跃可以覆盖的距离，如果距离大于等于长度，则可以实现跳跃到最后。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean canJump(int[] nums) {
        int cover = 0;
        if(nums.length == 1) return true;
        for(int i = 0; i <= cover; i++){
            cover = Math.max(i + nums[i], cover);
            if(cover >= nums.length - 1) return true;
        }
        return false;
    }
}
```

<br>

## 45. 跳跃游戏II
- 题目链接：[**LeetCode 45. Jump Game II**](https://leetcode.com/problems/jump-game-ii/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题跟55不同的点在于需要计算最短次数到达末尾。需要计算当前下标能到达的最远位置，如果最远位置是末尾，则次数不需要加1。如果不是末尾，则次数要加1。

<br>

## 💻 代码实现
```java
class Solution {
    public int jump(int[] nums) {
        int result = 0;
        int end = 0;
        int temp = 0;
        for(int i = 0; i <= end && end < nums.length - 1; i++){
            temp = Math.max(temp, i + nums[i]);
            if(i == end){
                end = temp;
                result++;
            }
        }
        return result;
    }
}
```

<br>

## 1005. K次取反后最大化的数组和
- 题目链接：[**LeetCode 1005. Maximize Sum of Array After K Negations**](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题要进行两次贪心算法。先是sort一次，把负数都变成正数。再sort一次后，把最小的数字变成相反数。

原理就在于，有些负数的绝对值会比正数的大，当k的值大于负数的个数时，只能将最小的几个正数变成负数。




<br>

## 💻 代码实现
```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        if(nums.length == 1) return nums[0];
        Arrays.sort(nums);
        for(int i = 0; i < nums.length && k > 0; i++){
            if(nums[i] < 0){
                nums[i] = -nums[i];
                k--;
            }
        }

        if(k % 2 == 1){
            Arrays.sort(nums);
            nums[0] = -nums[0];
        }

        int sum = 0;
        for(int num: nums){
            sum += num;
        }
        return sum;
    }
}
```

<br>

## 📝 今日心得
今天是对于贪心算法的一个介绍，有的题目的贪心算法就比较简单，有的就比较复杂，总体来讲就是看怎么能节省步骤，就是贪心的本质。