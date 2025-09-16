# 📝 LeetCode 学习日志 Day 21

<br>

## 669. 修剪二叉搜索树
- 题目链接：[**LeetCode 669. Trim a Binary Search Tree**](https://leetcode.com/problems/trim-a-binary-search-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题比较的有困难，思路就是，如果当前节点的值小于low，就要把当前节点的右边trim了之后return右边的root。如果当前节点的值大于high的话，就要把左边trim了之后return左边的root。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if(root == null) return null;
        if(root.val < low) return trimBST(root.right, low, high);
        if(root.val > high) return trimBST(root.left, low, high);

        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

<br>

## 108. 将有序数组转换为二叉搜索树  
- 题目链接：[**LeetCode 108. Convert Sorted Array to Binary Search Tree**](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。找到中间root的index，将这个array分成两部分，然后重复操作找root.left和root.right。


<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBST(nums, 0, nums.length);
    }

    public TreeNode sortedArrayToBST(int[] nums, int left, int right){
        if(left >= right) return null;
        if(right - left == 1) return new TreeNode(nums[left]);
        int middle = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums[middle]);
        root.left = sortedArrayToBST(nums, left, middle);
        root.right = sortedArrayToBST(nums, middle + 1, right);
        return root;
    }
}
```

<br>

## 538. 把二叉搜索树转换为累加树
- 题目链接：[**LeetCode 538. Convert BST to Greater Tree**](https://leetcode.com/problems/convert-bst-to-greater-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题可以参考538，采用右中左的方式完成，只要update value就行。

<br>

## 💻 代码实现
```java
class Solution {
    int sum;
    public TreeNode convertBST(TreeNode root) {
        sum = 0;
        convertBST1(root);
        return root;
    }

    public void convertBST1(TreeNode root){
        if(root == null) return;
        convertBST1(root.right);
        sum += root.val;
        root.val = sum;
        convertBST1(root.left);
    }
}
```

<br>

## 📝 今日心得
总体而言，今天的题目难度不是很大，但是自己在写recursion的感觉就是没有什么信心，思路很接近但是很难写出正确的代码，似乎知道怎么做但是还是差一口气，说明练习有效果但是还不够多。