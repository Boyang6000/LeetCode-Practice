# 📝 LeetCode 学习日志 Day 23

<br>

## 39. 组合总和
- 题目链接：[**LeetCode 39. Combination Sum**](https://leetcode.com/problems/combination-sum/)
- 关键词：**Backtracking**  

<br>

## 💡 思路
这道题也是使用了回溯算法，不过sum的update是通过parameter来update的，怎么让数字能重复选择呢，保持你的startIndex，这样每次递归的时候都是在同一个index上面寻找，进入下一个index是由for loop来控制。

<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);
        backtracking(candidates, target, 0, 0);
        return result;
    }

    public void backtracking(int[] candidates, int target, int sum, int startIndex){
        if(sum > target) return;
        if(sum == target){
            result.add(new ArrayList<>(path));
            return;
        }

        for(int i = startIndex; i < candidates.length ;i++){
            if(sum + candidates[i] > target) break;
            path.add(candidates[i]);
            backtracking(candidates, target, sum + candidates[i], i);
            path.removeLast();
        }
    }
}
```

<br>

## 40. 组合总和II
- 题目链接：[**LeetCode 40. Combination Sum II**](https://leetcode.com/problems/combination-sum-ii/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题跟39类似，先sort array然后加个去重就行。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    int sum = 0;

    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        backtracking(candidates, target, 0);
        return result;
    }

    public void backtracking(int[] candidates, int target, int startIndex){
        if(sum == target){
            result.add(new ArrayList<>(path));
            return;
        }

        for(int i = startIndex; i < candidates.length && sum < target; i++){
            if(i > startIndex && candidates[i-1] == candidates[i]) continue;
            path.add(candidates[i]);
            sum += candidates[i];
            backtracking(candidates, target, i + 1);
            int temp = path.getLast();
            sum -= temp;
            path.removeLast();
        }
    }
}
```

<br>

## 131. 分割回文串
- 题目链接：[**LeetCode 131. Palindrome Partitioning**](https://leetcode.com/problems/palindrome-partitioning/)
- 关键词：**Backtracking**

<br>

## 💡 思路
分割其实跟组合问题是一样的，都是可以通过回溯来解决的，这里只需要多加一个method来确认当前stringbuilder是否为回文就行了

<br>

## 💻 代码实现
```java
class Solution {
    List<List<String>> result = new ArrayList<>();
    List<String> cur = new ArrayList<>();
    public List<List<String>> partition(String s) {
        backtracking(s, 0, new StringBuilder());
        return result;
    }
    private void backtracking(String s, int start, StringBuilder sb){
        if(start == s.length()){
            result.add(new ArrayList<>(cur));
            return;
        }
        for(int i = start; i < s.length(); i++){
            sb.append(s.charAt(i));
            if(check(sb)){
                cur.add(sb.toString());
                backtracking(s, i + 1, new StringBuilder());
                cur.remove(cur.size() - 1);
            }
        }
    }

    private boolean check(StringBuilder sb){
        for(int i = 0; i < sb.length() / 2; i++){
            if(sb.charAt(i) != sb.charAt(sb.length() - i - 1)) return false;
        }
        return true;
    }
}
```

<br>

## 📝 今日心得
今天的题目是对回溯的一个练习，回溯和递归是类似的逻辑，理解起来会有些难度，回溯主要用在组合问题上，本质上也是一种brutal Force，还需多加练习才会熟练。