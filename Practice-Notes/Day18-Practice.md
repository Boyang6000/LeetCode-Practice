# 📝 LeetCode 学习日志 Day 18

<br>

## 530. 二叉搜索树的最小绝对差
- 题目链接：[**LeetCode 530. Minimum Absolute Difference in BST**](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题用的是recursion。跟98的思路类似，是一道很经典在二叉搜索树上用双指针的例子。先找到最左边的node设定为pre，然后拿他的root去跟他比较，比较完之后移动pre。

<br>

## 💻 代码实现
```java
class Solution {
    TreeNode pre;
    int min = Integer.MAX_VALUE;
    public int getMinimumDifference(TreeNode root) {
        if(root == null) return 0;
        traversal(root);
        return min;
    }

    public void traversal(TreeNode root){
        if(root == null) return;
        traversal(root.left);
        if(pre != null) min = Math.min(min, root.val - pre.val);
        pre = root;
        traversal(root.right);
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

 - **如果需要搜索整棵二叉树且不用处理递归返回值，递归函数就不要返回值。**
 - **如果需要搜索整棵二叉树且需要处理递归返回值，递归函数就需要返回值。**
 - **如果要搜索其中一条符合条件的路径，那么递归一定需要返回值，因为遇到符合条件的路径了就要及时返回。**