# 📝 LeetCode 学习日志 Day 14

<br>

## 226. 翻转二叉树
- 题目链接：[**LeetCode 226. Invert Binary Tree**](https://leetcode.com/problems/invert-binary-tree/)
- 关键词：**Recursion**  

<br>

## 💡 思路
这道题比较的简单，但是也需要理解明白其中的意思。最直接的就是用recursion的办法。以下的方法是采用了前序遍历的方法（中左右），先swap中间的node，再进行到他们的children。

<br>

## 💻 代码实现
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return root;
        swap(root);
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }

    public void swap(TreeNode root){
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
    }
}
```

<br>

## 101. 对称二叉树
- 题目链接：[**LeetCode 101. Symmetric Tree**](https://leetcode.com/problems/symmetric-tree/)
- 关键词：**Recursion**

<br>

## 💡 思路
这道题也是采用了recursion的方法。主要分析有以下几种情况：
 - 左为空，右不为空 -> false
 - 左不为空，右为空 -> false
 - 左为空，右为空 -> true
 - 左不为空，右不为空，但左右值不同 -> false

这样就可以继续这个recursion，看两边外侧是否相同，内侧是否相同，将最终的结果return回去。


<br>

## 💻 代码实现
```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return compare(root.left, root.right);
    }

    private boolean compare(TreeNode left, TreeNode right){
        if(left != null && right == null) return false;
        else if(left == null && right != null) return false;
        else if(left == null && right == null) return true;
        else if(left.val != right.val) return false;
        else{
            boolean outside = compare(left.left, right.right);
            boolean inside = compare(left.right, right.left);
            return outside && inside;
        }
    }
}
```

<br>

## 347.前 K 个高频元素
- 题目链接：[**LeetCode 347. Top K Frequent Elements**](https://leetcode.com/problems/top-k-frequent-elements/)
- 关键词：**PriorityQueue**

<br>

## 💡 思路
这道题比较的有难度，第一次做可能做不出来。这道题需要同时考虑出现频率最高的元素和出现的频率，所以这里采用的是Min-Heap的方式，通过PriorityQueue来实现。

先用一个Map来统计所有的元素以及他的出现频率，然后用PriorityQueue的方式，将元素和频率看作一个int数组，进行排序，当pq的size小于k，加入map里的元素，当size超过k时，如果新的元素频率大于pq里最小的频率，则update。最后将pq里的数字导出到一个int数组里。

<br>

## 💻 代码实现
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num: nums){
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

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

        int[] res = new int[k];

        for(int i = k-1; i >= 0; i--){
            res[i] = pq.poll()[0];
        }

        return res;
    }
}
```

<br>

## 📝 今日心得
今天的题目还是相对比较有难度的，第一次做的时候不容易想出来。今天做题时发现还是对stack和queue的一些功能不是很熟悉，比如push是stack用来加元素的，而queue会用add/offer，deque和queue一样，然后priorityqueue是用add。今天还涉及到了priorityqueue来实现Min-Heap，也算是复习和重新捡起印象，多练就会熟练了。