# 📝 LeetCode 学习日志 Day 10

<br>

## 232.用栈实现队列
- 题目链接：[**LeetCode 232. Implement Queue Using Stack**](https://leetcode.com/problems/implement-queue-using-stacks/)
- 关键词：**Queue, Stack**  

<br>

## 💡 思路
这道题就是考察对Queue和Stack的理解程度。建立两个Stack，StackIn和StackOut，然后push的时候push到StackIn，pop和peek时先把stackIn里面的数字push到stackOut里面，这样先加入到stackIn的数字（在stack的末尾）就会变成stackOut的最上面，实现了FIFO

<br>

## 💻 代码实现
```java
class MyQueue {
    Stack<Integer> stackIn;
    Stack<Integer> stackOut;

    public MyQueue() {
        stackIn = new Stack<>();
        stackOut = new Stack<>();
    }
    
    public void push(int x) {
        stackIn.push(x);
    }
    
    public int pop() {
        dumpstackIn();
        return stackOut.pop();
    }
    
    public int peek() {
        dumpstackIn();
        return stackOut.peek();
    }
    
    public boolean empty() {
        return stackIn.isEmpty() && stackOut.isEmpty();
    }

    private void dumpstackIn(){
        if(!stackOut.isEmpty()) return;
        while(!stackIn.isEmpty()){
            stackOut.push(stackIn.pop());
        }
    }
}
```

<br>

## 225. 用队列实现栈
- 题目链接：[**LeetCode 225. Implement Stack Using Queues**](https://leetcode.com/problems/implement-stack-using-queues/)
- 关键词：**Deque, ArrayDeque, Stack**

<br>

## 💡 思路
这道题用Deque中的ArrayDeque来实现，因为ArrayDeque可以在首位和末尾进行push，pop，peek，比较方便

这里面的offer跟push相同，push失败的时候会throw execption，offer失败时会return false。

这里在push的时候就将里面元素的顺序反过来了，满足stack先进后出的原则

<br>

## 💻 代码实现
```java
class MyStack {
    private Deque<Integer> q = new ArrayDeque<>();

    public void push(int x) {
        q.offer(x);
        for (int i = 0; i < q.size() - 1; i++) {
            q.offer(q.poll());
        }
    }

    public int pop() {
        return q.poll();
    }

    public int top() {
        return q.peek();
    }

    public boolean empty() {
        return q.isEmpty();
    }
}
```

<br>

## 20. 有效的括号
- 题目链接：[**LeetCode 20. Valid Parentheses**](https://leetcode.com/problems/valid-parentheses/description/)
- 关键词：**Deque, LinkedList**

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

## 📝 今日心得
今天的这两道KMP算法相当有难度，有时间时需要多复习加深印象，主要就是要理解Next数组是如何计算的，然后回退到前缀的index又是具体怎么操作的，第一次不理解没关系，重复多次硬啃下来还是可以的。