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