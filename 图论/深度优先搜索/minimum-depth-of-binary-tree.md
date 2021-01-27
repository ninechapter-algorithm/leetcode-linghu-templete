# 二叉树的最小深度
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-depth-of-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，找出其最小深度。

二叉树的最小深度为根节点到最近叶子节点的最短路径上的节点数量。
 ### 样例说明
 **样例 1:**

```
输入: {}
输出: 0
```

**样例 2:**

```
输入:  {1,#,2,3}
输出: 3	
解释:
	1
	 \ 
	  2
	 /
	3    
它将被序列化为 {1,#,2,3}
```

**样例 3:**

```
输入:  {1,2,3,#,#,4,5}
输出: 2	
解释: 
      1
     / \ 
    2   3
       / \
      4   5  
它将被序列化为 {1,2,3,#,#,4,5}
```
 ### 参考代码
 Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

考点：
* 二叉树遍历
* 搜索


题解：直接搜索给出的二叉树即可。
```java
public class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return getMin(root);
    }

    public int getMin(TreeNode root){
        if (root == null) {
            return Integer.MAX_VALUE;
        }

        if (root.left == null && root.right == null) {
            return 1;
        }

        return Math.min(getMin(root.left), getMin(root.right)) + 1;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)