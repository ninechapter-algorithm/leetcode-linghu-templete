# 二叉树的前序遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-preorder-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一棵二叉树，返回其节点值的前序遍历。</p>
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3}
输出：[1,2,3]
解释：
   1
  / \
 2   3
它将被序列化为{1,2,3}
前序遍历
```
**样例 2:**
```
输入：{1,#,2,3}
输出：[1,2,3]
解释：
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
前序遍历
```
 ### 参考代码
 Given a binary tree, return the preorder traversal of its nodes' values.&nbsp;<div><br></div><div>For example:&nbsp;</div><div>Given binary tree {1,#,2,3},&nbsp;</div><div><br></div><div>&nbsp;1&nbsp;</div><div>&nbsp; &nbsp;\&nbsp;</div><div>&nbsp; &nbsp; &nbsp;2&nbsp;</div><div>&nbsp; &nbsp; /&nbsp;</div><div>&nbsp; 3&nbsp;</div><div>return [1,2,3].&nbsp;</div><div><br></div><div>&nbsp;Note: Recursive solution is trivial, could you do it iteratively?</div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;"><br></span></div><div><span style="color: rgb(102, 110, 112); font-family: 'Open Sans', Arial, sans-serif; line-height: 22.3999996185303px;">详细题解请见九章算法微博：</span><font color="#666e70" face="Open Sans, Arial, sans-serif"><span style="line-height: 22.3999996185303px;"><a href="http://weibo.com/3948019741/BzQahxewZ" target="_blank">http://weibo.com/3948019741/BzQahxewZ</a></span></font><br></div>
考点：
* 二叉树的前序遍历

题解：
非递归方式实现前序遍历时，首先存入当前节点值，然后先将右儿子压入栈中，再将左儿子压入栈中。对栈中元素遍历访问。
```java
Version 0: Non-Recursion (Recommend)
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        List<Integer> preorder = new ArrayList<Integer>();
        
        if (root == null) {
            return preorder;
        }
        
        stack.push(root);
        while (!stack.empty()) {
            TreeNode node = stack.pop();
            preorder.add(node.val);
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        
        return preorder;
    }
}

//Version 1: Traverse
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        traverse(root, result);
        return result;
    }
    // 把root为跟的preorder加入result里面
    private void traverse(TreeNode root, ArrayList<Integer> result) {
        if (root == null) {
            return;
        }

        result.add(root.val);
        traverse(root.left, result);
        traverse(root.right, result);
    }
}

//Version 2: Divide & Conquer
public class Solution {
    public ArrayList<Integer> preorderTraversal(TreeNode root) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        // null or leaf
        if (root == null) {
            return result;
        }

        // Divide
        ArrayList<Integer> left = preorderTraversal(root.left);
        ArrayList<Integer> right = preorderTraversal(root.right);

        // Conquer
        result.add(root.val);
        result.addAll(left);
        result.addAll(right);
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)