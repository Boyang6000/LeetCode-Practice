# 📝 LeetCode 学习日志 Day 2

<br>

## 209. 长度最小的子数组
- 题目链接：[**LeetCode 209. Minimum Size Subarray Sum**](https://leetcode.com/problems/minimum-size-subarray-sum/)
- 关键词：**Sliding Window**  

<br>

## 💡 思路
这是练习滑动窗口比较基础的一道题目，设立一个指针指向最左边，然后通过循环依次将数字加入到sum里面去，当sum大于等于target的时候，通过依次减去左边的数字来缩小窗口并将满足的长度update  

<br>

## 💻 代码实现
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int minLength = Integer.MAX_VALUE;
        int left = 0;
        int sum = 0;
        
        for(int right = 0; right < nums.length; right++){
            sum += nums[right];
            while(sum >= target){
                minLength = Math.min(minLength, right - left + 1);
                sum -= nums[left];
                left++;
            }
        }

        return minLength == Integer.MAX_VALUE ? 0 : minLength;
    }
}
```

<br>

##  59. 螺旋矩阵II
- 题目链接：[**LeetCode 59. Spiral Matrix II**](https://leetcode.com/problems/spiral-matrix-ii/)
- 关键词：**Matrix**

<br>

## 💡 思路
这道题非常考察基本功，尤其是对循环的开始和结束节点的把握。首先先要判断这个matrix有几层，通过n/2来判断，然后将每一层的loop的开始点设为(startX,startY)，通过n-offset来设定每一段loop的结束点，然后以上右下左的顺序用四个loop来填写数字

这里面四个循环填数字和一个loop结束后update每个值会比较容易搞混和遗忘

另一个点就是要记住Matrix index的格式 (X,Y)

<br>

## 💻 代码实现
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] ans = new int[n][n];
        int startX = 0;
        int startY = 0;
        int offset = 1;
        int count = 1;
        int loop = 1;
        int i,j;

        while(loop <= n/2){
            for(j = startY; j < n - offset; j++){
                ans[startX][j] = count;
                count++;
            }

            for(i = startX; i < n - offset; i++){
                ans[i][j] = count;
                count++;
            }

            for(;j > startY; j--){
                ans[i][j] = count;
                count++;
            }

            for(; i > startX; i--){
                ans[i][startY] = count;
                count++;
            }

            startX++;
            startY++;
            offset++;
            loop++;

        }
           
        if(n % 2 == 1){
            ans[n/2][n/2] = n*n;
        }

        return ans;
    }
}
```

<br>

## 📝 今日心得
Sliding Window在数组当中还是比较实用的，通过sliding window可以将两个loop变成一个，缩短运行时间。第一题是一个很好的sliding window的例子。第二题加强了对于loop的运用，锻炼如何在多个循环中确认开始和结束的节点。