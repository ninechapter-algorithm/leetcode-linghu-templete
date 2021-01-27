# 验证二叉查找树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/validate-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，判断它是否是合法的二叉查找树(BST)

一棵BST定义为：

* 节点的左子树中的值要**严格**小于该节点的值。
* 节点的右子树中的值要**严格**大于该节点的值。
* 左右子树也必须是二叉查找树。
* 一个节点的树也是二叉查找树。
 ### 样例说明
 **样例 1:**
```
输入：{-1}
输出：true
解释：
二叉树如下(仅有一个节点）:
	-1
这是二叉查找树。
```	

**样例 2:**
```
输入：{2,1,4,#,#,3,5}
输出：true
解释：
	二叉树如下：
	  2
	 / \
	1   4
	   / \
	  3   5
这是二叉查找树。
```
 ### 参考代码
 分治法，但是 minValue 和 maxValue 用 minNode 和 maxNode 来代替。
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
    public boolean isBST;
    public TreeNode maxNode, minNode;
    public ResultType(boolean isBST) {
        this.isBST = isBST;
        this.maxNode = null;
        this.minNode = null;
    }
}

public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        return divideConquer(root).isBST;
    }
    
    private ResultType divideConquer(TreeNode root) {
        if (root == null) {
            return new ResultType(true);
        }
        
        ResultType left = divideConquer(root.left);
        ResultType right = divideConquer(root.right);
        if (!left.isBST || !right.isBST) {
            return new ResultType(false);
        }
        
        if (left.maxNode != null && left.maxNode.val >= root.val) {
            return new ResultType(false);
        }
        
        if (right.minNode != null && right.minNode.val <= root.val) {
            return new ResultType(false);
        }
        
        // is bst
        ResultType result = new ResultType(true);
        result.minNode = left.minNode != null ? left.minNode : root;
        result.maxNode = right.maxNode != null ? right.maxNode : root;
        
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)