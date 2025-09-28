# 📝 LeetCode 学习日志 Day 32

<br>

## 509. 斐波那契数
- 题目链接：[**LeetCode 509. Fibonacci Number**](https://leetcode.com/problems/fibonacci-number/)
- 关键词：**Dynamic Programming**  

<br>

## 💡 思路
这道题是dp里面最基础的一道题。

**动规五部曲：**

这里我们要用一个一维dp数组来保存递归的结果

 - 确定dp数组以及下标的含义：

     - **dp[i]的定义为：第i个数的斐波那契数值是dp[i]**

 - 确定递推公式
     - 为什么这是一道非常简单的入门题目呢？因为题目已经把递推公式直接给我们了：**状态转移方程 dp[i] = dp[i - 1] + dp[i - 2];**

 - dp数组如何初始化
     - **dp[0] = 0; dp[1] = 1;**
 
 - 确定遍历顺序
     - 从递归公式dp[i] = dp[i - 1] + dp[i - 2];中可以看出，dp[i]是依赖 dp[i - 1] 和 dp[i - 2]，那么遍历的顺序一定是**从前到后**遍历的

 - 举例推导dp数组
     - 按照这个递推公式dp[i] = dp[i - 1] + dp[i - 2]，我们来推导一下，当N为10的时候，dp数组应该是如下的数列：

        0 1 1 2 3 5 8 13 21 34 55
        
<br>

## 💻 代码实现
```java
class Solution {
    public int fib(int n) {
        if(n <= 1) return n;
        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for(int index = 2; index <= n; index++){
            dp[index] = dp[index - 1] + dp[index - 2];
        }
        return dp[n];
    }
}
```

<br>

## 738. 单调递增的数字
- 题目链接：[**LeetCode 738. Monotone Increasing Digits**](https://leetcode.com/problems/monotone-increasing-digits/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题比较的巧妙，需要通过倒序的方式来处理，当当前index的数字比后面的数字大时，当前index数字减1，后面的数字变成9。

为了方便操作，可以先把数字变成string模式，最后再把string变成int。


<br>

## 💻 代码实现
```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        String s = String.valueOf(n);
        char[] chars = s.toCharArray();
        int start = s.length();
        for(int i = s.length() - 2; i >= 0; i--){
            if(chars[i] > chars[i + 1]){
                chars[i]--;
                start = i + 1;
            }
        }
        for(int i = start; i < s.length(); i++){
            chars[i] = '9';
        }
        return Integer.parseInt(String.valueOf(chars));
    }
}
```

<br>

## 📝 今日心得
今天的内容都是处理重叠区域的，重点在于区域的划分，按照什么顺序来找。贪心算法还是很不好想的，当看到答案时又会发现其实思路是很简单的。