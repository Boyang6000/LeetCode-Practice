# 📝 LeetCode 学习日志 Day 9

<br>

## 151. 翻转字符串里的单词
- 题目链接：[**LeetCode 151. Reverse Words in a String**](https://leetcode.com/problems/reverse-words-in-a-string/)
- 关键词：**String, Two Pointers**  

<br>

## 💡 思路
这道题比较的繁琐，主要是有三个步骤：
 
 - 去除掉多余的空格：
     - 设定一个start指向string的开始，end指向string的末尾，先去除开始和结尾的空格，当start指向第一个字母和end指向最后一个字母时，创建一个新的StringBuilder，将所有字母加入进去，中间多的空格跳过。

 - 反转整个String：
     - 跟swap一样。

 - 反转每个单词：采用双指针的办法，设定start = 0， end = 1，然后先让end找到单词末尾的空格，然后在这个范围里进行反转整个String，然后移动start和end直至start和end到结尾。

<br>

## 💻 代码实现
```java
class Solution {
    public String reverseWords(String s) {
        StringBuilder sb = removeExtraSpace(s);
        reverseString(sb, 0, sb.length() - 1);
        reverseEachWord(sb);
        return sb.toString();
    }

    private StringBuilder removeExtraSpace(String s){
        int start = 0;
        int end = s.length() -1;
        while(s.charAt(start) == ' ') start++;
        while(s.charAt(end) == ' ') end--;
        StringBuilder sb = new StringBuilder();
        while(start <= end){
            char c = s.charAt(start);
            if(c != ' ' || s.charAt(start - 1) != ' '){
                sb.append(c);
            }
            start++;
        }
        return sb;
    }

    public void reverseString(StringBuilder sb, int start, int end){
        while(start < end){
            char temp = sb.charAt(start);
            sb.setCharAt(start, sb.charAt(end));
            sb.setCharAt(end, temp);
            start++;
            end--;
        }
    }

    public void reverseEachWord(StringBuilder sb){
        int start = 0;
        int end = 1;
        int n = sb.length();
        while(start < n){
            while(end < n && sb.charAt(end) != ' ') end++;
            reverseString(sb, start, end-1);
            start = end + 1;
            end = start + 1;
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

## 📝 今日心得
今天的这两道题就比较基础，都是运用到了swap来做字符串反转，像第二题的话就要注意边界值，多思考思考for loop里每一次index增加的量，不用一定要是i++，也可以是别的increment。