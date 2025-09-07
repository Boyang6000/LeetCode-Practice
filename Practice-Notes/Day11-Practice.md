# 📝 LeetCode 学习日志 Day 11

<br>

## 150. 逆波兰表达式求值
- 题目链接：[**LeetCode 150. Evaluate Reverse Polish Notation**](https://leetcode.com/problems/evaluate-reverse-polish-notation/)
- 关键词：**Stack**  

<br>

## 💡 思路
这道题相对而言比较简单，建立一个stack用ArrayDeque来实现，当这个token是数字时，加入到stack里面。当这个token是运算符号时，pop两个数字从stack里面，进行运算，然后把结果重新push到stack里面。最后stack剩下的那个数字就是结果了。

<br>

## 💻 代码实现
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i < tokens.length; i++) {
            String token = tokens[i];
            if (token.equals("+")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second + first);
            } else if (token.equals("-")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second - first);
            } else if (token.equals("*")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second * first);
            } else if (token.equals("/")) {
                int first = stack.pop();
                int second = stack.pop();
                stack.push(second / first);
            } else {
                stack.push(Integer.valueOf(token));
            }
        }
        return stack.pop();
    }
}
```

<br>

## 239. 滑动窗口最大值
- 题目链接：[**LeetCode 239. Sliding Window Maximum**](https://leetcode.com/problems/sliding-window-maximum/)
- 关键词：**Deque, ArrayDeque**

<br>

## 💡 思路
这道题比较的有难度。需要用到单调队列的思想。建立一个deque单调队列，从大到小来放index，当deque里第一个index不在sliding window的范围时poll出来。当deque的末尾数字小于将要加进去的数字时，将末尾数字poll出来，因为他永远不可能成为sliding window里最大的数字。将这个index加入到deque里面。当循环进入sliding window时，每一次移动窗口都把最大的数字，也就是deque的最前端，加入到答案里面去。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int length = nums.length;
        int[] ans = new int[length - k + 1];
        int count = 0;
        Deque<Integer> deque = new ArrayDeque<>();

        for(int i = 0; i < nums.length; i++){
            while(!deque.isEmpty() && deque.peek() < i - k + 1){
                deque.poll();
            }

            while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i]){
                deque.pollLast();
            }

            deque.offer(i);

            if(i >= k - 1){
                ans[count] = nums[deque.peek()];
                count++;
            }
        }

        return ans;
    }
}
```

<br>

## 20. 有效的括号
- 题目链接：[**LeetCode 20. Valid Parentheses**](https://leetcode.com/problems/valid-parentheses/description/)
- 关键词：**Deque, ArrayDeque**

<br>

## 💡 思路
这道题就是对于stack的运用，stack通常在括号匹配中使用，这里我们通过ArrayDeque来实现stack的功能。

当遇到一个左括号时，我们就把相对应的右括号加入到stack里面。

三种情况会return false：
 - 左括号多于右括号
 - 右括号多于左括号
 - 括号类型不匹配

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (ch == '(') stack.push(')');
            else if (ch == '{') stack.push('}');
            else if (ch == '[') stack.push(']');
            else if (stack.isEmpty() || stack.peek() != ch) return false;
            else stack.pop();
        }
        return stack.isEmpty();
    }
}

```

<br>

## 1047. 删除字符串中的所有相邻重复项
- 题目链接：[**LeetCode 1047. Remove All Adjacent Duplicates in String**](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
- 关键词：**ArrayDeque**

<br>

## 💡 思路
这道题也是一个stack的运用，这里用ArrayDeque来实现stack的功能。

先创建一个ArrayDeque，如果stack里面最后一位跟即将加入的字母一样，那么直接去除最后一位。如果不是前面这种情况则直接加入新的字母。最后将stack里面的字母转化为string。

<br>

## 💻 代码实现
```java
class Solution {
    public String removeDuplicates(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for(int i = 0; i < s.length(); i++){
            if(!stack.isEmpty() && stack.peekLast() == s.charAt(i)){
                stack.pollLast();
            }
            else{
                stack.addLast(s.charAt(i));
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (char c : stack) {
            sb.append(c);
            }
        return sb.toString();
    }
}

```

<br>

## 📝 今日心得
对于stack和queue的实现还是不太熟悉和熟练。基本上用的最多的就是Deque来实现stack和queue，因为他可以在两端增加删除element，其中用的比较多的就是ArrayDeque，LinkedList用的少一些。可以多加练习和熟练每个类型里面可以使用的method。