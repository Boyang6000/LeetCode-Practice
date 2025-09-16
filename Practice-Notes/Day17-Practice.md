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

## 112. 路径总和
- 题目链接：[**LeetCode 112. Path Sum**](https://leetcode.com/problems/path-sum/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。不要去计算这一条path上的sum，而是去做减法。当targetSum等于0且当前node是叶子时return true。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if(root == null) return false;
        targetSum -= root.val;
        if(root.left == null && root.right == null) return targetSum == 0;
        boolean left = hasPathSum(root.left, targetSum);
        if(left) return true;
        boolean right = hasPathSum(root.right, targetSum);
        if(right) return true;
        return false;
    }
}
```

<br>

## 113. 路径总和 II
- 题目链接：[**LeetCode 113. Path Sum II**](https://leetcode.com/problems/path-sum-ii/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题跟112的思路有一些不同，因为需要记录所有等于targetSum的path。

也是采用recursion的方法，创建一个result来记录所有符合要求的path，创建一个path来记录可能的路径。当左右child都是null和targetSum变成0时，把这个path加入到result里面。不满足时则回退一个node继续寻找。

<br>

## 💻 代码实现
```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> result = new ArrayList<>();
        if(root == null) return result;
        List<Integer> path = new LinkedList<>();
        preorderDFS(root, targetSum, result, path);
        return result;
    }

    public void preorderDFS(TreeNode node, int targetSum, List<List<Integer>> result, List<Integer> path){
        if (node == null) return;
        path.add(node.val);
        int remain = targetSum - node.val;
        if(node.left == null && node.right == null){
            if(remain == 0){
                result.add(new ArrayList<>(path));
            }
            return;
        }
        
        if(node.left != null){
            preorderDFS(node.left, remain, result, path);
            path.remove(path.size() - 1);
        }
        if(node.right != null){
            preorderDFS(node.right, remain, result, path);
            path.remove(path.size() - 1);
        }
    }
}
```

<br>

## 106. 从中序与后序遍历序列构造二叉树
- 题目链接：[**LeetCode 106. Construct Binary Tree from Inorder and Postorder Traversal**](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。重点在于怎么找root node，已知后序遍历的顺序是左右中，这样的话最后一个就是root。又知道中序遍历是左中右，那么通过寻找到root可以把中序分成左中序和右中序两个部分。根据这两个部分的长度，可以找出后序遍历中左后序和右后序的部分，接着进行recursion。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if(inorder.length == 0 || postorder.length == 0) return null;
        return buildHelper(inorder, 0, inorder.length, postorder, 0, postorder.length);
    }
    
    private TreeNode buildHelper(int[] inorder, int inorderStart, int inorderEnd, int[] postorder, int postorderStart, int postorderEnd){
        if(postorderStart == postorderEnd) return null;
        int rootVal = postorder[postorderEnd - 1];
        TreeNode root = new TreeNode(rootVal);
        int middleIndex;
        for(middleIndex = inorderStart; middleIndex < inorderEnd; middleIndex++){
            if(inorder[middleIndex] == rootVal) break;
        }

        int leftInOrderStart = inorderStart;
        int leftInOrderEnd = middleIndex;
        int rightInOrderStart = middleIndex + 1;
        int rightInOrderEnd = inorderEnd;

        int leftPostOrderStart = postorderStart;
        int leftPostOrderEnd = postorderStart + (middleIndex - inorderStart);
        int rightPostOrderStart = leftPostOrderEnd;
        int rightPostOrderEnd = postorderEnd - 1;
        
        root.left = buildHelper(inorder, leftInOrderStart, leftInOrderEnd, postorder, leftPostOrderStart, leftPostOrderEnd);
        root.right = buildHelper(inorder, rightInOrderStart, rightInOrderEnd, postorder, rightPostOrderStart, rightPostOrderEnd);

        return root;
    }
}
```

<br>

## 105. 从前序与中序遍历序列构造二叉树
- 题目链接：[**LeetCode 105. Construct Binary Tree from PreOrder and Inorder Traversal**](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题的思路与106相同。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder == null || inorder == null) return null;
        return buildHelper(preorder, 0, preorder.length, inorder, 0, inorder.length);
    }

    private TreeNode buildHelper(int[] preorder, int preorderStart, int preorderEnd, int[] inorder, int inorderStart, int inorderEnd){
        if(preorderStart == preorderEnd) return null;
        int rootVal = preorder[preorderStart];
        TreeNode root = new TreeNode(rootVal);
        int middleIndex;

        for(middleIndex = inorderStart; middleIndex < inorderEnd; middleIndex++){
            if(inorder[middleIndex] == rootVal) break;
        }

        int leftInOrderStart = inorderStart;
        int leftInOrderEnd = middleIndex;
        int rightInOrderStart = middleIndex + 1;
        int rightInOrderEnd = inorderEnd;
        
        int leftPreOrderStart = preorderStart + 1;
        int leftPreOrderEnd = preorderStart + 1 + (middleIndex - inorderStart);
        int rightPreOrderStart = leftPreOrderEnd;
        int rightPreOrderEnd = preorderEnd;

        root.left = buildHelper(preorder, leftPreOrderStart, leftPreOrderEnd, inorder, leftInOrderStart, leftInOrderEnd);
        root.right = buildHelper(preorder, rightPreOrderStart, rightPreOrderEnd, inorder, rightInOrderStart, rightInOrderEnd);

        return root;
    }
}
```

<br>

## 📝 今日心得
今天的题目重点采用了recursion的方法去写，可以发现用recursion的话在大部分二叉树的题目上都很省力。**重点就还是在以下三点：**

- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**
