# 📝 LeetCode 学习日志 Day 28

<br>

## 122.买卖股票的最佳时机II
- 题目链接：[**LeetCode 122. Best Time to Buy and Sell Stock II**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题采用了贪心算法,是一个非常巧妙的思路。因为只能有一股，当前只有买股票和卖股票两个操作，那么可以把利润分解到每天为单位的维度

例如你在第0天买，第3天卖，那么利润就是prices[3] - prices[0] = (prices[3] - prices[2]) + (prices[2] - prices[1]) + (prices[1] - prices[0])

最后只要把利润是正的加在一起就行。


<br>

## 💻 代码实现
```java
class Solution {
    public int maxProfit(int[] prices) {
        int[] profit = new int[prices.length - 1];
        int index = 0;
        int sum = 0;
        for(int i = 1; i < prices.length; i++){
            profit[index] = prices[i] - prices[index];
            if(profit[index] > 0){
                sum += profit[index];
            }
            index++;
        }
        return sum;
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

## 📝 今日心得
今天是对于贪心算法的一个介绍，有的题目的贪心算法就比较简单，有的就比较复杂，总体来讲就是看怎么能节省步骤，就是贪心的本质。