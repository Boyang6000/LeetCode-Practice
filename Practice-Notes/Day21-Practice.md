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

## 450. 删除二叉搜索树中的节点 
- 题目链接：[**LeetCode 450. Delete Node in a BST**](https://leetcode.com/problems/delete-node-in-a-bst/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题用的是recursion来删除节点，重点是考虑以下五种情况：

***没找到删除的节点***
 - **第一种情况：遍历到空节点直接返回了**

***找到删除的节点***

 - **第二种情况：左右孩子都为空（叶子节点），直接删除节点， 返回NULL为根节点**
 - **第三种情况：删除节点的左孩子为空，右孩子不为空，删除节点，右孩子补位，返回右孩子为根节点**
 - **第四种情况：删除节点的右孩子为空，左孩子不为空，删除节点，左孩子补位，返回左孩子为根节点**
 - **第五种情况：左右孩子节点都不为空，则将删除节点的左子树头结点（左孩子）放到删除节点的右子树的最左面节点的左孩子上，返回删除节点右孩子为新的根节点。**

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if(root == null) return root;
        if(root.val == key){
            if(root.left == null) return root.right;
            else if(root.right == null) return root.left;
            else{
                TreeNode cur = root.right;
                while(cur.left != null){
                    cur = cur.left;
                }
                cur.left = root.left;
                root = root.right;
                return root;
            }
        }

        if(root.val > key) root.left = deleteNode(root.left, key);
        if(root.val < key) root.right = deleteNode(root.right, key);
        return root;
    }
}
```

<br>

## 📝 今日心得
总体而言，今天的题目难度不是很大，但是自己在写recursion的感觉就是没有什么信心，不知道是要return值还是不return，需要多多思考recursion的写法多加练习。