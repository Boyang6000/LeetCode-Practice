# 📝 LeetCode 学习日志 Day 16

<br>

## 513. 找树左下角的值
- 题目链接：[**LeetCode 513. Find Bottom Left Tree Value**](https://leetcode.com/problems/find-bottom-left-tree-value/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题用层序遍历会比recursion方便很多，只要每次update第一个node的值就行了，因为第一个node永远都是左node。

<br>

## 💻 代码实现
```java
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if(root == null) return 0;
        queue.offer(root);
        int ans = 0;
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                if(i == 0) ans = temp.val;
                if(temp.left != null) queue.offer(temp.left);
                if(temp.right != null) queue.offer(temp.right);
            }
        }
        return ans;
    }
}
```

<br>

## 257. 二叉树的所有路径
- 题目链接：[**LeetCode 257. Binary Tree Paths**](https://leetcode.com/problems/binary-tree-paths/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。主要用到StringBuilder来进行node的添加。如果node的左右child都是null，那就是到了叶子，就只要把node.val加进去就行。其他情况则加入node.val和->。


<br>

## 💻 代码实现
```java
class Solution {
    List<String> result = new ArrayList<>();
    public List<String> binaryTreePaths(TreeNode root) {
        makePath(root, "");
        return result;
    }

    public void makePath(TreeNode node, String s){
        if(node == null) return;
        if(node.left == null && node.right == null){
            result.add(new StringBuilder(s).append(node.val).toString());
            return;
        }
        String temp = new StringBuilder(s).append(node.val).append("->").toString();
        makePath(node.left, temp);
        makePath(node.right, temp);
    }
}
```

<br>

## 404. 左叶子之和
- 题目链接：[**LeetCode 404. Sum of Left Leaves**](https://leetcode.com/problems/sum-of-left-leaves/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。重点在于怎么判断他是左叶子，当这个father node有一个left child，然后这个child的左右两边都是null，则这个就是个左叶子。

<br>

## 💻 代码实现
```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null) return 0;
        if(root.left == null && root.right == null) return 0;
        int left = sumOfLeftLeaves(root.left);
        if(root.left != null && root.left.left == null && root.left.right == null) left = root.left.val;
        int right = sumOfLeftLeaves(root.right);
        int sum = left + right;
        return sum;
    }
}
```

<br>

## 222. 完全二叉树的节点个数
- 题目链接：[**LeetCode 222. Count Complete Tree Nodes**](https://leetcode.com/problems/count-complete-tree-nodes/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题采用了recursion的办法，变得简单灵巧。这个是通用算完全二叉树/满二叉树的解法。只需要采用recursion把node数量相加return就行。

<br>

## 💻 代码实现
```java
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null) {
            return 0;
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}
```

<br>

## 📝 今日心得
今天的题目重点采用了recursion的方法去写，慢慢能抓到recursion是怎么写的了。**重点就还是在以下三点：**

- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**
