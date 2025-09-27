# 📝 LeetCode 学习日志 Day 25

<br>

## 491. 递增子序列 
- 题目链接：[**LeetCode 491. Non Decreasing Subsequences**](https://leetcode.com/problems/non-decreasing-subsequences/)
- 关键词：**Backtracking**  

<br>

## 💡 思路
这道题也是运用了回溯法来实现的。这里需要注意两点，第一点是检查path size是不是大于1，如果是的话就把这个path放到result里面。其次是判断nums[i]是否加入到path里面。如果nums[i]小于path最后一位，则不加入；如果nums[i]已经用过了（用used数组来判断是否用过），则不考虑加入。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> findSubsequences(int[] nums) {
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        if(path.size() > 1){
            result.add(new ArrayList<>(path));
        }
        int[] used = new int[201];
        for(int i = startIndex; i < nums.length; i++){
            if(!path.isEmpty() && nums[i] < path.get(path.size() - 1) || (used[nums[i] + 100] == 1)){
                continue;
            }
            used[nums[i] + 100] = 1;
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.remove(path.size() - 1);
        }
    }
}
```

<br>

## 46. 全排列
- 题目链接：[**LeetCode 46. Permutations**](https://leetcode.com/problems/permutations/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题就是比较基础的backtracking运用, 对于重复的数字，这里可以运用到linkedlist里面的method contains来检查是否已经选取过元素。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> permute(int[] nums) {
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        if(path.size() == nums.length){
            result.add(new ArrayList<>(path));
        }
        for(int i = startIndex; i < nums.length; i++){
            if(path.contains(nums[i])){
                continue;
            }
            path.add(nums[i]);
            backtracking(nums, startIndex);
            path.removeLast();
        }
    }
}
```

<br>

## 90. 子集II
- 题目链接：[**LeetCode 90. Subsets II**](https://leetcode.com/problems/subsets-ii/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题的思路跟78是一样的，只不过多了一个去重，去重之前需要先把array sort一下，这样当当前index的数字和前一个index数字相同时，直接continue。

<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        backtracking(nums, 0);
        return result;
    }

    private void backtracking(int[] nums, int startIndex){
        result.add(new ArrayList<>(path));
        for(int i = startIndex; i < nums.length; i++){
            if(i > startIndex && nums[i] == nums[i - 1]) continue;
            path.add(nums[i]);
            backtracking(nums, i + 1);
            path.removeLast();
        }
    }
}
```

<br>

## 📝 今日心得
今天的题目是对回溯的一个练习，回溯和递归是类似的逻辑，理解起来会有些难度，需要熟练掌握回溯的写法，对于不同情况的运用随机应变。