# 二叉树的后序遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-postorder-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一棵二叉树，返回其节点值的后序遍历。</p>
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3}
输出：[2,3,1]
解释： 
   1
  / \
 2   3
它将被序列化为{1,2,3}
后序遍历
```
**样例 2:**
```
输入：{1,#,2,3}
输出：[3,2,1]
解释： 
1
 \
  2
 /
3
它将被序列化为{1,#,2,3}
后序遍历
```
 ### 参考代码
 Given a binary tree, return the postorder traversal of its nodes' values.&nbsp;<div>For example:&nbsp;</div><div>Given binary tree {1,#,2,3},<div><br></div><div>1<div>&nbsp; \&nbsp;</div><div>&nbsp; &nbsp;2&nbsp;</div><div>&nbsp; /&nbsp;</div><div>&nbsp;3&nbsp;</div><div><br></div><div>return [3,2,1].&nbsp;</div><div><br></div><div>&nbsp;Note: Recursive solution is trivial, could you do it iteratively?</div></div></div><div><br></div><div>九章算法微博：<a href="http://weibo.com/3948019741/Bq8XobZFD" target="_blank">面试搞定二叉树大总结</a></div>
考点：
* 二叉树的后序遍历
题解：
使用栈进行二叉树后序遍历，首先对左子树进行遍历压入栈中，直至左子树为空，然后访问右子树。故每个节点会被访问两次，当节点被第二次访问时，该节点出栈。
```java
//Recursive
public ArrayList<Integer> postorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();

    if (root == null) {
        return result;
    }

    result.addAll(postorderTraversal(root.left));
    result.addAll(postorderTraversal(root.right));
    result.add(root.val);

    return result;   
}

//Iterative
public ArrayList<Integer> postorderTraversal(TreeNode root) {
    ArrayList<Integer> result = new ArrayList<Integer>();
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode prev = null; // previously traversed node
    TreeNode curr = root;

    if (root == null) {
        return result;
    }

    stack.push(root);
    while (!stack.empty()) {
        curr = stack.peek();
        if (prev == null || prev.left == curr || prev.right == curr) { // traverse down the tree
            if (curr.left != null) {
                stack.push(curr.left);
            } else if (curr.right != null) {
                stack.push(curr.right);
            }
        } else if (curr.left == prev) { // traverse up the tree from the left
            if (curr.right != null) {
                stack.push(curr.right);
            }
        } else { // traverse up the tree from the right
            result.add(curr.val);
            stack.pop();
        }
        prev = curr;
    }

    return result;
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)