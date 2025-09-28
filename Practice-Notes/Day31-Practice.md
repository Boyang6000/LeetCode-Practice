# 📝 LeetCode 学习日志 Day 31

<br>

## 56. 合并区间
- 题目链接：[**LeetCode 56. Merge Intervals**](https://leetcode.com/problems/merge-intervals/)
- 关键词：**Greedy**  

<br>

## 💡 思路
这道题其实跟452和435是一样的。先确定两个interval是否重合，如果重合，就调整interval的末尾来cover两个interval。如果不重合就直接把这个interval加入到result里面。

<br>

## 💻 代码实现
```java
class Solution {
    public int[][] merge(int[][] intervals) {
        List<int[]> result = new LinkedList<>();
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));
        result.add(intervals[0]);
        for(int i = 1; i < intervals.length; i++){
            if(intervals[i][0] <= result.getLast()[1]){
                int start = result.getLast()[0];
                int end = Math.max(intervals[i][1], result.getLast()[1]);
                result.removeLast();
                result.add(new int[]{start, end});
            }
            else{
                result.add(intervals[i]);
            }
        }
        return result.toArray(new int[result.size()][]);
    }
}
```

<br>

## 435. 无重叠区间
- 题目链接：[**LeetCode 435. Non-overlapping Intervals**](https://leetcode.com/problems/non-overlapping-intervals/)
- 关键词：**Greedy**

<br>

## 💡 思路
这道题采用的是贪心算法，跟452类似，只要减去箭的个数就是不重复的了。


<br>

## 💻 代码实现
```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        Arrays.sort(intervals, (a, b) -> Integer.compare(a[0], b[0]));

        int count = 1;
        for(int i = 1; i < intervals.length; i++){
            if(intervals[i][0] < intervals[i-1][1]){
                intervals[i][1] = Math.min(intervals[i][1], intervals[i-1][1]);
            }
            else{
                count++;
            }
        }
        return intervals.length - count;
    }
}
```

<br>

## 763. 划分字母区间 
- 题目链接：[**LeetCode 763. Partition Labels**](https://leetcode.com/problems/partition-labels/)
- 关键词：**Greedy**

<br>

## 💡 思路
先找出每个字母出现的最迟的index，然后进行for loop，当当前index等于最迟index时，说明可以分割字母串，将这个字母串的长度放到list里面。

<br>

## 💻 代码实现
```java
class Solution {
    public List<Integer> partitionLabels(String s) {
        List<Integer> list = new LinkedList<>();
        int[] edge = new int[26];
        char[] chars = s.toCharArray();
        for(int i = 0; i < chars.length; i++){
            edge[chars[i] - 'a'] = i;
        }
        int idx = 0;
        int last = -1;
        for(int i = 0; i < chars.length; i++){
            idx = Math.max(idx, edge[chars[i] - 'a']);
            if(i == idx){
                list.add(i - last);
                last = i;
            }
        }
        return list;
    }
}
```

<br>

## 📝 今日心得
今天的内容都是处理重叠区域的，重点在于区域的划分，按照什么顺序来找。