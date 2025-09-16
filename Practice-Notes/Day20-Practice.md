# 📝 LeetCode 学习日志 Day 20

<br>

## 235. 二叉搜索树的最近公共祖先 
- 题目链接：[**LeetCode 235. Minimum Absolute Difference in BST**](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题跟235略微不同因为二叉搜索树的特性，当root第一次出现在pq interval之间时，他就是最近公共祖先。

为什么呢？因为当root第一次出现在pq interval之间时，继续往root.left或者root.right探索，只会寻找到p或者q，不能同时找到pq，所以继续往下探寻找不到公共祖先。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root.val > p.val && root.val > q.val) return lowestCommonAncestor(root.left, p, q);
        if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
        return root;
    }
}
```

<br>

## 701. 二叉搜索树中的插入操作
- 题目链接：[**LeetCode 701. Insert into a Binary Search Tree**](https://leetcode.com/problems/insert-into-a-binary-search-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。当当前root值大于val，就在左边寻找；当当前root值小于val，就在右边寻找。


<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root == null){
            root = new TreeNode(val);
            return root;
        }
        if(root.val > val) root.left = insertIntoBST(root.left, val);
        if(root.val < val) root.right = insertIntoBST(root.right, val);
        return root;
    }
}
```

<br>

## 236. 二叉树的最近公共祖先 
- 题目链接：[**LeetCode 236. Lowest Common Ancestor of a Binary Tree**](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题比较困难，用到的是recursion里面的回溯。首先我们是用的后序遍历（左右中），然后当找到p或者q时，return p或者q。当左右两边都是null时，说明没找到pq，return null。当有一边不为null时，return那一边的value。当两边都不是null时，说明找到了pq，那就return他们的root。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q) return root;

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left == null && right == null) return null;
        else if(left != null && right == null) return left;
        else if(left == null && right != null) return right;
        else return root;
    }
}
```

<br>

## 📝 今日心得
今天的题目还是比较的有难度的，涉及到了在二叉搜索树里用双指针，还有就是回溯。当需要从下往上去遍历时，就用后序遍历。