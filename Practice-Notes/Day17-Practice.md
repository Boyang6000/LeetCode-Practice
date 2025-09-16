# 📝 LeetCode 学习日志 Day 17

<br>

## 654. 最大二叉树
- 题目链接：[**LeetCode 654. Maximum Binary Tree**](https://leetcode.com/problems/maximum-binary-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题用的是recursion。重复的去找最大值，然后在最大值的左右两边重复这个过程。注意要判断interval里面是否存在有效node。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return constructHelper(nums, 0, nums.length);
    }

    public TreeNode constructHelper(int[] nums, int leftIndex, int rightIndex){
        if(rightIndex - leftIndex < 1) return null;
        if(rightIndex - leftIndex == 1) return new TreeNode(nums[leftIndex]);

        int maxIndex = leftIndex;
        int maxValue = nums[leftIndex];
        for(int i = leftIndex + 1; i < rightIndex; i++){
            if(nums[i] > maxValue) {
                maxValue = nums[i];
                maxIndex = i;
            }
        }

        TreeNode root = new TreeNode(maxValue);
        root.left = constructHelper(nums, leftIndex, maxIndex);
        root.right = constructHelper(nums, maxIndex + 1, rightIndex);
        return root;
    }
}
```

<br>

## 617. 合并二叉树
- 题目链接：[**LeetCode 617. Merge Two Binary Trees**](https://leetcode.com/problems/merge-two-binary-trees/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。当其中一个node是null的时候，return另一个node就行。


<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
        if(root1 == null) return root2;
        if(root2 == null) return root1;
        
        TreeNode root = new TreeNode(root1.val + root2.val);
        root.left = mergeTrees(root1.left, root2.left);
        root.right = mergeTrees(root1.right, root2.right);
        return root;
    }
}
```

<br>

## 700. 二叉搜索树中的搜索
- 题目链接：[**LeetCode 700. Search In a Binary Search Tree**](https://leetcode.com/problems/search-in-a-binary-search-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题比较的简单，用recursion或者迭代都可以完成。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if(root == null) return null;
        else if(root.val > val) return searchBST(root.left, val);
        else if(root.val < val) return searchBST(root.right, val);
        else return root;
    }
}
```

<br>

## 98. 验证二叉搜索树
- 题目链接：[**LeetCode 98. Validate Binary Search Tree**](https://leetcode.com/problems/validate-binary-search-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用的是recursion，用的是中序遍历的方式（左中右），先找到最左边的node，然后再一个个向上比较看当前node是否大于前驱node，大于的话update前驱node为当前node。

<br>

## 💻 代码实现
```java
class Solution {
    TreeNode max;
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;

        boolean left = isValidBST(root.left);
        if(!left) return false;

        if(max != null && root.val <= max.val) return false;
        max = root;

        boolean right = isValidBST(root.right);
        return right; 
    }
}
```

<br>

## 📝 今日心得
今天的题目重点采用了recursion的方法去写，可以发现用recursion的话在大部分二叉树的题目上都很省力，今天的题目相对比较的简单，需要注意的是要判断recursion method的return，判断是void，return一个值，还是return boolean，就会有不同的写法。**重点就还是在以下三点：**

- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**
