# 翻转二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/invert-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 翻转一棵二叉树。左右子树交换。
 ### 样例说明
 **样例 1:**

```
输入: {1,3,#}
输出: {1,#,3}
解释:
	  1    1
	 /  =>  \
	3        3
```

**样例 2:**
```
输入: {1,2,3,#,#,4}
输出: {1,3,2,#,4}
解释: 
	
      1         1
     / \       / \
    2   3  => 3   2
       /       \
      4         4
```
 ### 参考代码
 考点：
* 二叉树
* 搜索

题解：
递归过程中直接交换当前节点的左右子树，构造新的二叉树返回即可。
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
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        if (root == null) {
            return;
        }
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        invertBinaryTree(root.left);
        invertBinaryTree(root.right);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)