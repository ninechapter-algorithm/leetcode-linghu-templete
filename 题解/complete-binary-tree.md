# 完全二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/complete-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 判断一个二叉树是否是完全二叉树
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3,4}
输出：true
解释：
        1
       / \
      2   3
     /
    4

是完全二叉树。
```
**样例 2:**
```
输入：{1,2,3,#,4}
输出：false
解释：
        1
       / \
      2   3
       \
        4

不是完全二叉树
```
 ### 参考代码
 根据每个结点的左子树和右子树的深度和是否满判断该结点的子树的类型
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
 
class ResultType {
    public int depth;
    public boolean isFull, isComplete;
    ResultType(int depth, boolean isFull, boolean isComplete) {
        this.depth = depth;
        this.isFull = isFull;
        this.isComplete = isComplete;
    }
}

public class Solution {
    /**
     * @param root, the root of binary tree.
     * @return true if it is a complete binary tree, or false.
     */
    public boolean isComplete(TreeNode root) {
        ResultType result = helper(root);
        return result.isComplete;
    }
    
    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, true, true);
        }
        
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        if (!left.isComplete) {
            return new ResultType(-1, false, false);
        }
        
        // depth is the same, left should be full and right should be complete
        if (left.depth == right.depth) {
            if (!left.isFull || !right.isComplete) {
                return new ResultType(-1, false, false);
            }
            return new ResultType(left.depth + 1, right.isFull, true);
        }
        
        // left.depth = right.depth + 1, left should be complete and right should be full
        if (left.depth == right.depth + 1) {
            if (!left.isComplete || !right.isFull) {
                return new ResultType(-1, false, false);
            }
            return new ResultType(left.depth + 1, false, true);
        }
        
        return new ResultType(-1, false, false);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)