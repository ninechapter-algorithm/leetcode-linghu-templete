# 二叉树的层次遍历 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-level-order-traversal-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一棵二叉树，返回其节点值从底向上的层次序遍历（按从叶节点所在层到根节点所在的层遍历，然后逐层从左往右遍历）</p>
 ### 样例说明
 例1:
```
输入:
{1,2,3}
输出:
[[2,3],[1]]
解释:
    1
   / \
  2   3
它将被序列化为 {1,2,3}
层次遍历
```
例2:
```
输入:
{3,9,20,#,#,15,7}
输出:
[[15,7],[9,20],[3]]
解释:
    3
   / \
  9  20
    /  \
   15   7
它将被序列化为 {3,9,20,#,#,15,7}
层次遍历
```

 ### 参考代码
 利用队列层序遍历整棵树，最后翻转一下即可。
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
     * @param root: The root of binary tree.
     * @return: buttom-up level order a list of lists of integer
     */
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                level.add(head.val);
                if (head.left != null) {
                    queue.offer(head.left);
                }
                if (head.right != null) {
                    queue.offer(head.right);
                }
            }
            result.add(level);
        }
        
        Collections.reverse(result);
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)