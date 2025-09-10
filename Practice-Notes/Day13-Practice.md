# 📝 LeetCode 学习日志 Day 13

<br>

## 144. 二叉树的前序遍历
- 题目链接：[**LeetCode 144. Binary Tree Preorder Traversal**](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion**  

<br>

## 💡 思路

<br>

## 💻 代码实现

### 递归法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result =  new ArrayList<>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
```

<br>

## 145. 二叉树的后序遍历
- 题目链接：[**LeetCode 145. Binary Tree Postorder Traversal**](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- 关键词：**Binary Tree, Postorder, Recursion**

<br>

## 💡 思路


<br>

## 💻 代码实现
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        postorder(root, result);
        return result;
    }

    public void postorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        postorder(root.left, result);
        postorder(root.right, result);
        result.add(root.val);
    }
}
```

<br>

## 94. 二叉树的中序遍历
- 题目链接：[**LeetCode 94. Binary Tree Inorder Traversal**](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- 关键词：**Binary Tree, Inorder, Traversal**

<br>

## 💡 思路


<br>

## 💻 代码实现
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorder(root, result);
        return result;
    }

    public void inorder(TreeNode root, List<Integer> result){
        if(root == null) return;
        inorder(root.left, result);
        result.add(root.val);
        inorder(root.right, result);
    }
}
```

<br>

## 📝 今日心得
