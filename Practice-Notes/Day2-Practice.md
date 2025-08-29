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
