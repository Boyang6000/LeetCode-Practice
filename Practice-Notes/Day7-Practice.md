# 📝 LeetCode 学习日志 Day 7

<br>

## 454. 四数相加II
- 题目链接：[**LeetCode 454. 4 Sum II**](https://leetcode.com/problems/4sum-ii/)
- 关键词：**HashMap**  

<br>

## 💡 思路
这道题就是比较经典需要用到HashMap的题目，先将前两个数相加，然后把相加的结果和出现次数放到HashMap里面，再把后两个数相加的相反数算出来，看这个相反数在HashMap里出现几次，将次数加到最终答案里。

<br>

## 💻 代码实现
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        int count = 0;
        Map<Integer, Integer> check = new HashMap<>();
        
        for(int i: nums1){
            for(int j: nums2){
                int sum = i + j;
                check.put(sum, check.getOrDefault(sum, 0) + 1);
            }
        }

        for(int m: nums3){
            for(int n: nums4){
                count += check.getOrDefault(0-m-n, 0);
            }
        }

        return count;
    }
}
```

<br>

## 383. 赎金信
- 题目链接：[**LeetCode 383. Ransom Note**](https://leetcode.com/problems/ransom-note/)
- 关键词：**List**

<br>

## 💡 思路
本题和 242.有效的字母异位词 是一个思路, 建立一个int list，然后将ransomNote字母出现的次数放到list里面，再把magazine字母出现的次数减去，最后看list里面是否有大于0的数字，大于0说明不满足条件。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) {
            return false;
        }
        int[] check = new int[26];

        for(int i = 0; i < ransomNote.length(); i++){
            check[ransomNote.charAt(i) - 'a']++;
        }
        for(int j = 0; j < magazine.length(); j++){
            check[magazine.charAt(j) - 'a']--;
        }
        for(int i: check){
            if(i > 0){
                return false;
            }
        }
        return true;
    }
}
```

<br>

##  202. 快乐数
- 题目链接：[**LeetCode 202. Happy Number**](https://leetcode.com/problems/happy-number/)
- 关键词：**HashSet**

<br>

## 💡 思路  
这道题先要去理解什么情况下是happy number什么情况下不是。当运算结果等于1的时候就是happy number，如果运算过程中出现了重复结果就不是。储存每次结果跟重复挂钩时优先考虑HashSet。

这道题分为两步：
- 先写一个method来运算happy。先算这个数字mod10剩下的余数，就是最右边的这个digit。然后平方再加入到sum里面去，最后将这个数字除以10，就进入到下一个digit的运算。重复循环直至所有digit的平方都加入到了sum里面。
- 主要的method来看这个数字是否是happy number。先创建一个HashSet来储存所有出现的结果。当这个数字不等于1或者没有出现在HashSet里面时，将他加入到HashSet里，然后再进行happy运算，重复这个过程。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean isHappy(int n) {
        Set<Integer> check = new HashSet<>();
        while(n != 1 && !(check.contains(n))){
            check.add(n);
            n = happy(n);
        }

        return n == 1;
    }

    public int happy(int n){
        int sum = 0;
        while(n > 0){
            int digit = n % 10;
            sum += digit * digit;
            n = n / 10;
        }
        return sum;
    }
}
```

<br>

##  1. 两数之和
- 题目链接：[**LeetCode 1. Two Sum**]（https://leetcode.com/problems/two-sum/）
- 关键词：**HashMap**

<br>

## 💡 思路  
这道题是好几道经典题目的开始，比如三数之和和四数之和。创建一个HashMap来储存数字和他的index。计算target和当前index数字的差，如果他们的差在这个HashMap里，就return这两个数字的index。如果不在这个HashMap里面，就将当前的数字和他的index加入到HashMap里面。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> check = new HashMap<>();
        
        for(int i = 0; i < nums.length; i++){
            int diff = target - nums[i];
            if(check.containsKey(diff)){
                return new int[]{check.get(diff), i};
            }
            else{
                check.put(nums[i], i);
            }
        }

        return null;
    }
}
```

<br>

## 📝 今日心得
HashMap和HashSet一直以来就是我比较薄弱的地方，一方面是平时运用的少，另一方面是自己内心里还是有点恐惧这个题型，需要更多的练习巩固加强对HashMap和HashSet的运用。今天主要是帮助分别在什么情况下运用HashMap和HashSet，当需要考虑过滤重复值的时候运用HashSet，然后当需要考虑存储两个值，例如数字和他的index时，就需要运用HashMap。