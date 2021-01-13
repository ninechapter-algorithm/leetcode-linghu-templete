# 在二叉查找树中插入节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/insert-node-in-a-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一棵二叉查找树和一个新的树节点，将节点插入到树中。

你需要保证该树仍然是一棵二叉查找树。
 ### 样例说明
 ```
样例  1:
	输入: tree = {}, node= 1
	输出: {1}
	
	样例解释:
	在空树中插入一个点，应该插入为根节点。

	
样例 2:
	输入: tree = {2,1,4,3}, node = 6
	输出: {2,1,4,3,6}
	
	样例解释: 
	如下：
	
	  2             2
	 / \           / \
	1   4   -->   1   4
	   /             / \ 
	  3             3   6
	
```

 ### 参考代码
 在树上定位要插入节点的位置。
1. 如果它大于当前根节点，则应该在右子树中，如果没有右子树则将该点作为右儿子插入；若存在右子树则在右子树中继续定位。
2. 如果它小于当前根节点，则应该在左子树中，处理同上。

（二叉查找树中保证不插入已经存在的值）
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
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param node: insert this node into the binary search tree
     * @return: The root of the new binary search tree.
     */
    public TreeNode insertNode(TreeNode root, TreeNode node) {
        if (root == null) {
            return node;
        }
        if (root.val > node.val) {
            root.left = insertNode(root.left, node);
        } else {
            root.right = insertNode(root.right, node);
        }
        return root;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)