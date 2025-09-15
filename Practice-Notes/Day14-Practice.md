# 📝 LeetCode 学习日志 Day 14

<br>

## 110. 平衡二叉树
- 题目链接：[**LeetCode 110. Balanced Binary Tree**](https://leetcode.com/problems/balanced-binary-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题是通过recursion的方式。先写recursion method，如果左右高度差大于1，就return -1，不是的话就return当前高度，最后看这个recursion是不是return -1。

<br>

## 💻 代码实现
```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return getHeight(root) != -1;
    }

    public int getHeight(TreeNode root){
        if(root == null) return 0;
        int leftHeight = getHeight(root.left);
        if(leftHeight == -1) return -1;
        int rightHeight = getHeight(root.right);
        if(rightHeight == -1) return -1;

        if(Math.abs(leftHeight - rightHeight) > 1) return -1;
        return Math.max(leftHeight, rightHeight) + 1;
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

<<<<<<< HEAD
## 404. 左叶子之和
- 题目链接：[**LeetCode 404. Sum of Left Leaves**](https://leetcode.com/problems/sum-of-left-leaves/)
- 关键词：**Recursion**
=======
## 347.前 K 个高频元素
- 题目链接：[**LeetCode 347. Top K Frequent Elements**](https://leetcode.com/problems/top-k-frequent-elements/)
- 关键词：**PriorityQueue**
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)

<br>

## 💡 思路
<<<<<<< HEAD
这道题采用了recursion的办法，变得简单灵巧。重点在于怎么判断他是左叶子，当这个father node有一个left child，然后这个child的左右两边都是null，则这个就是个左叶子。
=======
这道题比较的有难度，第一次做可能做不出来。这道题需要同时考虑出现频率最高的元素和出现的频率，所以这里采用的是Min-Heap的方式，通过PriorityQueue来实现。

先用一个Map来统计所有的元素以及他的出现频率，然后用PriorityQueue的方式，将元素和频率看作一个int数组，进行排序，当pq的size小于k，加入map里的元素，当size超过k时，如果新的元素频率大于pq里最小的频率，则update。最后将pq里的数字导出到一个int数组里。
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)

<br>

## 💻 代码实现
```java
class Solution {
<<<<<<< HEAD
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
=======
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num: nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)

        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);
        for(Map.Entry<Integer, Integer> entry: map.entrySet()){
            if(pq.size() < k){
                pq.add(new int[]{entry.getKey(), entry.getValue()});
            }
            else{
                if(entry.getValue() > pq.peek()[1]){
                    pq.poll();
                    pq.add(new int[]{entry.getKey(), entry.getValue()});
                }
            }
        }

<<<<<<< HEAD
## 222. 完全二叉树的节点个数
- 题目链接：[**LeetCode 222. Count Complete Tree Nodes**](https://leetcode.com/problems/count-complete-tree-nodes/)
- 关键词：**Recursion**
=======
        int[] res = new int[k];
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)

        for(int i = k-1; i >= 0; i--){
            res[i] = pq.poll()[0];
        }

<<<<<<< HEAD
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
=======
        return res;
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)
    }
}
```

<br>

## 📝 今日心得
<<<<<<< HEAD
今天的题目重点采用了recursion的方法去写，慢慢能抓到recursion是怎么写的了。**重点就还是在以下三点：**

- **确定递归函数的参数和返回值**
- **确定终止条件**
- **确定单层递归的逻辑**
=======
今天的题目还是相对比较有难度的，第一次做的时候不容易想出来。今天做题时发现还是对stack和queue的一些功能不是很熟悉，比如push是stack用来加元素的，而queue会用add/offer，deque和queue一样，然后priorityqueue是用add。今天还涉及到了priorityqueue来实现Min-Heap，也算是复习和重新捡起印象，多练就会熟练了。
>>>>>>> parent of ad432fa (upload 104 and 111 for day 14)
