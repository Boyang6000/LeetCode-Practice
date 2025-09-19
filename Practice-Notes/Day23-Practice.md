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

## 216. 组合总和III  
- 题目链接：[**LeetCode 216. Combination Sum III**](https://leetcode.com/problems/combination-sum-iii/description/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题跟77的思路类似，就是要添加一个parameter sum。


<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        backtracking(k, n, 1, 0);
        return result;
    }

    public void backtracking(int k, int n, int startIndex, int sum){
        if(sum > n) return;
        if(path.size() == k){
            if(sum == n){
                result.add(new ArrayList<>(path));
                return;
            }
        }

        for(int i = startIndex; i <= 9 - (k - path.size()) + 1; i++){
            path.add(i);
            sum += i;
            backtracking(k, n, i+1, sum);
            path.removeLast();
            sum -= i;
        }
    }
}
```

<br>

## 17. 电话号码的字母组合
- 题目链接：[**LeetCode 17. Letter Combinations of a Phone Numberr**](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
- 关键词：**Backtracking**

<br>

## 💡 思路
这道题相对有点难度，先把0-9变成一个string array，然后把每个数字代表的字母放到这个array里面，进行backtracking。

<br>

## 💻 代码实现
```java
class Solution {
    List<String> list = new ArrayList<>();
    public List<String> letterCombinations(String digits) {
        if(digits == null || digits.length() == 0) return list;
        String[] numString = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
        backtracking(digits, numString, 0);
        return list;
    }

    StringBuilder temp = new StringBuilder();
    public void backtracking(String digits, String[] numString, int num){
        if(num == digits.length()){
            list.add(temp.toString());
            return;
        }

        String str = numString[digits.charAt(num) - '0'];
        for(int i = 0; i < str.length(); i++){
            temp.append(str.charAt(i));
            backtracking(digits, numString, num + 1);
            temp.deleteCharAt(temp.length() -1);
        }
    }
}
```

<br>

## 📝 今日心得
今天的题目是对回溯的一个介绍，回溯和递归是类似的逻辑，理解起来会有些难度，回溯主要用在组合问题上，本质上也是一种brutal Force，还需多加练习才会熟练。