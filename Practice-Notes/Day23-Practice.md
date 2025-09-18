# 📝 LeetCode 学习日志 Day 22

<br>

## 77. 修剪二叉搜索树
- 题目链接：[**LeetCode 77. Combinations**](https://leetcode.com/problems/combinations/)
- 关键词：**Backtracking**  

<br>

## 💡 思路
这道题是回溯算法的一个开始，也是最基础的用到回溯算法的问题。首先，确定回溯算法的终止条件，就是数组的size正好是k。其次单层搜索的逻辑就是用一个for循环来加入元素， 选取了第一个元素之后，对接下来的元素再进行递归。最后还得进行一次回溯，删除掉元素。

<br>

## 💻 代码实现
```java
class Solution {
    List<List<Integer>> result = new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> combine(int n, int k) {
        backtracking(n, k, 1);
        return result;
    }

    public void backtracking(int n, int k, int startIndex){
        if(path.size() == k){
            result.add(new ArrayList(path));
            return;
        }

        for(int i = startIndex; i <= n - (k - path.size()) + 1; i++){
            path.add(i);
            backtracking(n, k, i + 1);
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