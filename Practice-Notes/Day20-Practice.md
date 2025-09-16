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

## 501. 二叉搜索树中的众数
- 题目链接：[**LeetCode 501. Find Mode in Binary Search Tree**](https://leetcode.com/problems/find-mode-in-binary-search-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。相对来说还是比较有难度的，因为二叉搜索树的特性，我们可以不用map，然后只遍历一次就能得出所有众数。

创建一个count和maxCount，当pre是null或者root和pre不一样时，count重新回到1，一样的话count就增加。当每次count大于maxCount时，清除掉list里面的所有数字，把当前出现次数最多的数字加入到list里面，然后update maxCount。当count等于maxCount时，把当前node的值加入到list里面。


<br>

## 💻 代码实现
```java
class Solution {
    int maxCount;
    int count;
    ArrayList<Integer> resList;
    TreeNode pre;

    public int[] findMode(TreeNode root) {
        resList = new ArrayList<>();
        maxCount = 0; 
        count = 0;
        pre = null;
        findHelper(root);
        int[] res = new int[resList.size()];
        for(int i = 0; i < resList.size(); i++){
            res[i] = resList.get(i);
        }
        return res;
    }

    public void findHelper(TreeNode root){
        if(root == null) return;
        findHelper(root.left);

        int rootValue = root.val;
        if(pre == null || rootValue != pre.val){
            count = 1;
        }
        else{
            count++;
        }

        if(count > maxCount){
            resList.clear();
            resList.add(rootValue);
            maxCount = count;
        }
        else if(count == maxCount) resList.add(rootValue);
        pre = root;

        findHelper(root.right);
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