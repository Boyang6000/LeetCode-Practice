# 📝 LeetCode 学习日志 Day 36

<br>

## 1049. 最后一块石头的重量 II
- 题目链接：[**LeetCode 1049. Last Stone Weight II**](https://leetcode.com/problems/last-stone-weight-ii/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题用到的是01背包的方法，跟416是一样的，将这堆石头分成两个相同的重量，那他们互相相撞的结果就是剩下最小的重量了。

那么就是看最多能装多少重量，设定背包容量为总重量的一半。


<br>

## 💻 代码实现
```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int sum = 0;
        for(int stone: stones){
            sum += stone;
        }
        int target = sum >> 1;

        int[] dp = new int[target + 1];
        for(int i = 0; i < stones.length; i++){
            for(int j = target; j >= stones[i]; j--){
                dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
            }
        }

        return sum - 2*dp[target];
    }
}
```

<br>

## 📝 今日心得
背包问题非常的深奥，里面的变化也是特别多的。今天认真学习了01背包的二维数组实现和一维数组的实现。因为二维数组的公式推导是由左上的值和上方的值进行推导，压缩到一维数组里可以理解为复制了上方的数组，然后再和左上的值进行推导，这里的重点在于背包容量循环是倒序，如果是正序的话，物品会被添加多次，导致数据不准确。