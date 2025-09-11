# 📝 LeetCode 学习日志 Day 13

<br>

## 144. 二叉树的前序遍历
- 题目链接：[**LeetCode 144. Binary Tree Preorder Traversal**](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**  

<br>

## 💡 思路
首先，我们要知道**前序遍历**的顺序：**中左右**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。因为stack是后入先出，然后前序遍历的顺序是中左右，所以我们会先将中间node加入到结果里面，因为中是需要立即访问的，然后我们会先把右边加入到stack里面，再把左边加入到stack里面，确保左边node会先进行遍历。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。
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

### 迭代法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        if(root == null) return result;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if(node.right != null) stack.push(node.right);
            if(node.left != null) stack.push(node.left);
        }
        return result;
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                if(node.right != null) stack.push(node.right);
                if(node.left != null) stack.push(node.left);
                stack.push(node);
                stack.push(null);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 145. 二叉树的后序遍历
- 题目链接：[**LeetCode 145. Binary Tree Postorder Traversal**](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**

<br>

## 💡 思路
首先，我们要知道**后序遍历**的顺序：**左右中**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。因为stack是后入先出，然后后序遍历的顺序是左右中，所以我们会先将中间node加入到结果里面，因为中是需要立即访问的，然后我们会先把左边加入到stack里面，再把右边加入到stack里面，最后整个reverse，就得到了顺序左右中。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。

<br>

## 💻 代码实现

### 递归法

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

### 迭代法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        if(root == null) return result;
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.pop();
            result.add(node.val);
            if(node.left != null) stack.push(node.left);
            if(node.right != null) stack.push(node.right);
        }
        Collections.reverse(result);
        return result;    
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                stack.push(node);
                stack.push(null);
                if(node.right != null) stack.push(node.right);
                if(node.left != null) stack.push(node.left);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 94. 二叉树的中序遍历
- 题目链接：[**LeetCode 94. Binary Tree Inorder Traversal**](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- 关键词：**Binary Tree, Preorder, Recursion, Iteration, Stack**

<br>

## 💡 思路
首先，我们要知道**中序遍历**的顺序：**左中右**

**递归法**:
- 采用Recursion的方式，先写出一个recursion的method，然后在call这个method。这种方式是通过系统栈来实现的

**迭代法**：
- 这个是通过自己创建的stack来实现的。=中序遍历的迭代法和前后序的不同，他是先将左边所有的node一个个加入到stack里面，然后再pop出来加入右边node。

**统一迭代法**：
- 使用统一迭代法是因为如果用普通的迭代法的话，中序遍历的逻辑跟前后序遍历的逻辑不一样，会相对麻烦一些。采用统一迭代法的话可以让三个逻辑统一。
- 统一迭代法的逻辑就是将node以倒序的形式加入到stack里面，在中node加入之后加入一个null node。这个null node表示这个node的所有children都已经访问完了，接下来可以加入这个node的值到result里了。这样保证了前中后序的逻辑是一样的。

<br>

## 💻 代码实现

### 递归法

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

### 迭代法

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while(cur != null || !stack.isEmpty()){
            if(cur != null){
                stack.push(cur);
                cur = cur.left;
            }
            else{
                cur = stack.pop();
                result.add(cur.val);
                cur = cur.right;
            }
        }
        return result;
    }
}
```

### 统一迭代法

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        if(root != null) stack.push(root);
        while(!stack.isEmpty()){
            TreeNode node = stack.peek();
            if(node != null){
                stack.pop();
                if(node.right != null) stack.push(node.right);
                stack.push(node);
                stack.push(null);
                if(node.left != null) stack.push(node.left);
            }
            else{
                stack.pop();
                node = stack.pop();
                result.add(node.val);
            }
        }
        return result;
    }
}
```

<br>

## 102. 二叉树的层序遍历
- 题目链接：[**LeetCode 102. Binary Tree Level Order Traversal**](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- 关键词：**Binary Tree, Recursion**

<br>

## 💡 思路
这道题是采用了recursion的办法来实现BFS遍历整个tree。

先创建一个通用的resList，然后创建一个BFS method。如果当前node是null，就直接return，不是的话层数加1。如果resList的size小于层数，说明答案里面的int list不够多，就增加一个list到resList里面去。最后把node的值放到相对应的resList里的list里面，然后重复recursion。

<br>

## 💻 代码实现


```java
class Solution {
    List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        BFS(root);
        return resList;
    }

    public void BFS(TreeNode node){
        Queue<TreeNode> queue = new LinkedList<>();
        if(node == null) return;
        queue.offer(node);

        while(!queue.isEmpty()){
            List<Integer> item = new ArrayList<>();
            int len = queue.size();
            while(len > 0){
                TreeNode tempNode = queue.poll();
                item.add(tempNode.val);

                if(tempNode.left != null) queue.offer(tempNode.left);
                if(tempNode.right != null) queue.offer(tempNode.right);

                len--;
            }
            resList.add(item);
        }
    }
}
```

## 📝 今日心得
