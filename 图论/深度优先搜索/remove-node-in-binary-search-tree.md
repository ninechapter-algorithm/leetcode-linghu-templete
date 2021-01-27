# 删除二叉查找树的节点
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/remove-node-in-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定一棵具有不同节点值的二叉查找树，删除树中与给定值相同的节点。如果树中没有相同值的节点，就不做任何处理。你应该保证处理之后的树仍是<span style="line-height: 1.42857143;">二叉查找树。</span></p>
 ### 样例说明
 **样例1**

```plain
输入: 
Tree = {5,3,6,2,4}
k = 3
输出: {5,2,6,#,4} 或 {5,4,6,2}
说明:
给定了以下二叉搜索树:
    5
   / \
  3   6
 / \
2   4
移去3，你可以返回:
    5
   / \
  2   6
   \
    4
或
    5
   / \
  4   6
 /
2
```

**样例2**

```plain
输入: 
Tree = {5,3,6,2,4}
k = 4
输出: {5,3,6,2}
说明:
给定了以下二叉搜索树:
    5
   / \
  3   6
 / \
2   4
移去4，你应该返回
    5
   / \
  3   6
 /
2
```


 ### 参考代码
 Remove Node in Binary Search Tree
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
     * @param value: Remove the node with given value.
     * @return: The root of the binary search tree after removal.
     */
    public TreeNode removeNode(TreeNode root, int value) {
        TreeNode dummy = new TreeNode(0);
        dummy.left = root;
        
        TreeNode parent = findNode(dummy, root, value);
        TreeNode node;
        if (parent.left != null && parent.left.val == value) {
            node = parent.left;
        } else if (parent.right != null && parent.right.val == value) {
            node = parent.right;
        } else {
            return dummy.left;
        }
        
        deleteNode(parent, node);
        
        return dummy.left;
    }
    
    private TreeNode findNode(TreeNode parent, TreeNode node, int value) {
        if (node == null) {
            return parent;
        }
        
        if (node.val == value) {
            return parent;
        }
        if (value < node.val) {
            return findNode(node, node.left, value);
        } else {
            return findNode(node, node.right, value);
        }
    }
    
    private void deleteNode(TreeNode parent, TreeNode node) {
        if (node.right == null) {
            if (parent.left == node) {
                parent.left = node.left;
            } else {
                parent.right = node.left;
            }
        } else {
            TreeNode temp = node.right;
            TreeNode father = node;
            
            while (temp.left != null) {
                father = temp;
                temp = temp.left;
            }
            
            if (father.left == temp) {
                father.left = temp.right;
            } else {
                father.right = temp.right;
            }
            
            if (parent.left == node) {
                parent.left = temp;
            } else {
                parent.right = temp;
            }
            
            temp.left = node.left;
            temp.right = node.right;
        }
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)