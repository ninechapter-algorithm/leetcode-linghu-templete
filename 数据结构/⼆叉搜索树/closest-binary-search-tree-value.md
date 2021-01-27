# 二叉搜索树中最接近的值
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/closest-binary-search-tree-value/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵非空二叉搜索树以及一个target值，找到在BST中最接近给定值的节点值
 ### 样例说明
 **样例1**

```
输入: root = {5,4,9,2,#,8,10} and target = 6.124780
输出: 5
解释：
二叉树 {5,4,9,2,#,8,10}，表示如下的树结构：
        5
       / \
     4    9
    /    / \
   2    8  10
```



**样例2**

```
输入: root = {3,2,4,1} and target = 4.142857
输出: 4
解释：
二叉树 {3,2,4,1}，表示如下的树结构：
     3
    / \
  2    4
 /
1
```
 ### 参考代码
 算法很简单，求出 lowerBound 和 upperBound。即 < target 的最大值和 >= target 的最小值。
然后在两者之中去比较谁更接近，然后返回即可。

时间复杂度为 $O(h)$，注意如果你使用 in-order traversal 的化，时间复杂度会是 $o(n)$ 并不是最优的。另外复杂度也不是 $O(logn)$ 因为BST 并不保证树高是 logn 的。
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return 0;
        }
        
        TreeNode lowerNode = lowerBound(root, target);
        TreeNode upperNode = upperBound(root, target);
        
        if (lowerNode == null) {
            return upperNode.val;
        }
        
        if (upperNode == null) {
            return lowerNode.val;
        }
        
        if (target - lowerNode.val > upperNode.val - target) {
            return upperNode.val;
        }
        
        return lowerNode.val;
    }
    
    // find the node with the largest value that smaller than target
    private TreeNode lowerBound(TreeNode root, double target) {
        if (root == null) {
            return null;
        }
        
        if (target <= root.val) {
            return lowerBound(root.left, target);
        }
        
        // root.val < target
        TreeNode lowerNode = lowerBound(root.right, target);
        if (lowerNode != null) {
            return lowerNode;
        }
        
        return root;
    }
    
    // find the node with the smallest value that larger than or equal to target
    private TreeNode upperBound(TreeNode root, double target) {
        if (root == null) {
            return null;
        }
        
        if (root.val < target) {
            return upperBound(root.right, target);
        }
        
        // root.val >= target
        TreeNode upperNode = upperBound(root.left, target);
        if (upperNode != null) {
            return upperNode;
        }
        
        return root;
    }
    
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)