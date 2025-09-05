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

## 28. 实现 strStr()
- 题目链接：[**LeetCode 28. Find the Index of the First Occurance in a String**](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)
- 关键词：**KMP Algorithm**

<br>

## 💡 思路
这道题是非常经典用到KMP算法的，KMP主要运用在字符串匹配上，KMP的主要思想是**当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，可以利用这些信息避免从头再去做匹配了**。KMP算法是相当有难度去理解的，主要运用到的就是Next数组，也就是前缀表。

Next数组该如何实现呢？在这道题当中，设定一个指针指向前缀的末尾，另一个指针循环指向后缀的末尾，当前后缀末尾相等时，前缀末尾指针increment,直至最后，这样模式串的前缀表就生成好了。

然后开始进行字符串匹配，当出现字符串不匹配时，模式串会跳回之前一个index前缀的字符来继续进行匹配。

这就是KMP的算法精髓了。

<br>

## 💻 代码实现
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0) return 0;
        int[] next = new int[needle.length()];
        getNext(next, needle);

        int j = 0;
        for(int i = 0; i < haystack.length(); i++){
            while(j > 0 && needle.charAt(j) != haystack.charAt(i)){
                j = next[j - 1];
            }
            if(needle.charAt(j) == haystack.charAt(i)){
                j++;
            }
            if(j == needle.length()){
                return i - needle.length() + 1;
            }
        }
        return -1;
    }

    public void getNext(int[] next, String needle){
        int j = 0;
        next[0] = 0;
        for(int i = 1; i < needle.length(); i++){
            while(j > 0 && needle.charAt(i) != needle.charAt(j)){
                j = next[j-1];
            }
            if(needle.charAt(i) == needle.charAt(j)){
                j++;
            }
            next[i] = j;
        }
    }
}
```

<br>

## 459. 重复的子字符串
- 题目链接：[**LeetCode 459. Repeated Substring Pattern**](https://leetcode.com/problems/repeated-substring-pattern/)
- 关键词：**KMP Algorithm**

<br>

## 💡 思路
这道题同28一样也是运用到了KMP算法。关于KMP算法的应用可以详细看28题。

这道题先创建了next数组表，然后看最后一个数字的前缀是否满足重复：
 - 是否大于0
 - 整个长度减去前缀之后是否还能被整个长度整除

<br>

## 💻 代码实现
```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int[] next = new int[s.length()];
        int j = 0;
        int n = s.length();
        next[0] = 0;
        for(int i = 1; i < n; i++){
            while(j > 0 && s.charAt(i) != s.charAt(j)){
                j = next[j-1];
            }
            if(s.charAt(i) == s.charAt(j)){
                j++;
            }
            next[i] = j;
        }
        
        if (next[n - 1] > 0 && n % (n - next[n - 1]) == 0) {
            return true; 
        } 
        else {
            return false;
        }
    }
}
```

<br>

## 📝 今日心得
今天的这两道KMP算法相当有难度，有时间时需要多复习加深印象，主要就是要理解Next数组是如何计算的，然后回退到前缀的index又是具体怎么操作的，第一次不理解没关系，重复多次硬啃下来还是可以的。