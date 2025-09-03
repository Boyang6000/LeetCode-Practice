# 📝 LeetCode 学习日志 Day 8

<br>

## 344. 反转字符串
- 题目链接：[**LeetCode 344. Reverse String**](https://leetcode.com/problems/reverse-string/)
- 关键词：**String**  

<br>

## 💡 思路
这个就是最基础的swap的运用，设定一个temp来储存值，然后将左边的值放到temp里面，再把右边的值赋给左边，最后把temp的值赋给右边就行

<br>

## 💻 代码实现
```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;

        while(left < right){
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
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

##  15. 三数之和
- 题目链接：[**LeetCode 15. 3Sum**](https://leetcode.com/problems/3sum/)
- 关键词：**Two Pointers**

<br>

## 💡 思路  
这道题用Two Pointers会比较快捷。先将整个list sort，然后从第一个数字开始循环，先判断第一个数字是不是大于0，如果大于0的话，因为已经排过序了，所以后续不可能有数字满足这个条件。再判断第一个数字是否跟之前做过循环的数字有重复，重复就跳过。确认完毕之后进入双指针环节，设定left为i+1， right为右边最后一个数字，然后看他们的sum跟0的关系来调整left and right。满足条件之后放入答案里，再对left和right进行去重，重复就跳过。

<br>

## 💻 代码实现
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i++){
            if(nums[i] > 0){
                return ans;
            }
            if(i > 0 && nums[i-1] == nums[i]){
                continue;
            }

            int left = i + 1;
            int right = nums.length - 1;
            while(left < right){
                int sum = nums[i] + nums[left] + nums[right];
                if(sum > 0){
                    right--;
                }
                else if(sum < 0){
                    left++;
                }
                else{
                    ans.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while(left < right && nums[left] == nums[left + 1]){
                        left++;
                    }
                    while(left < right && nums[right - 1] == nums[right]){
                        right--;
                    }

                    left++;
                    right--;
                }
            } 
        }
        return ans;
    }
}
```

<br>

##  18. 四数之和
- 题目链接：[**LeetCode 18. 4Sum**]（https://leetcode.com/problems/4sum/）
- 关键词：**Two Pointers**

<br>

## 💡 思路  
这道题跟三数之和一样的，只不过就是多加一层循环。

<br>

## 💻 代码实现
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i++){
            if(nums[i] > target && nums[i] > 0){
                return ans;
            }
            if(i > 0 && nums[i-1] == nums[i]){
                continue;
            }
            for(int j = i + 1; j < nums.length; j++){
                if(nums[i] + nums[j] > target && nums[i] + nums[j] > 0){
                    break;
                }
                if(j > i+1 && nums[j-1] == nums[j]){
                    continue;
                }

                int left = j+1;
                int right = nums.length - 1;
                while(left < right){
                    int sum = nums[i] + nums[j] + nums[left] + nums[right];
                    if(sum > target){
                        right--;
                    }
                    else if(sum < target){
                        left++;
                    }
                    else{
                        ans.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        while(left < right && nums[left] == nums[left+1]) left++;
                        while(left < right && nums[right-1] == nums[right]) right--;
                        left++;
                        right--;
                    }
                }
            }
        }
        return ans;
    }
}
```

<br>

## 📝 今日心得
三数之和和四数之和虽然看起来代码量比较吓人，但实际理解起来没有那么复杂，多多练习对于edge case的敏感度。HashMap和HashSet的一些特殊method，像getOrDefault这些，也需要多练多记。