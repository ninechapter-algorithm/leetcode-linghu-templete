# 二叉树的锯齿形层次遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-zigzag-level-order-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给出一棵二叉树，返回其节点值的锯齿形层次遍历（先从左往右，下一层再从右往左，层与层之间交替进行）&nbsp;</p>
 ### 样例说明
 **样例 1:**
```
输入:{1,2,3}
输出:[[1],[3,2]]
解释:
    1
   / \
  2   3
它将被序列化为 {1,2,3}
```
**样例 2:**
```
输入:{3,9,20,#,#,15,7}
输出:[[3],[20,9],[15,7]]
解释:
    3
   / \
  9  20
    /  \
   15   7
它将被序列化为 {3,9,20,#,#,15,7}
```

 ### 参考代码
 层序遍历完之后，看层数，偶数层reverse一下即可。
```java
public class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();

        if (root == null) {
            return result;
        }

        Stack<TreeNode> currLevel = new Stack<TreeNode>();
        Stack<TreeNode> nextLevel = new Stack<TreeNode>();
        Stack<TreeNode> tmp;
        
        currLevel.push(root);
        boolean normalOrder = true;

        while (!currLevel.isEmpty()) {
            ArrayList<Integer> currLevelResult = new ArrayList<Integer>();

            while (!currLevel.isEmpty()) {
                TreeNode node = currLevel.pop();
                currLevelResult.add(node.val);

                if (normalOrder) {
                    if (node.left != null) {
                        nextLevel.push(node.left);
                    }
                    if (node.right != null) {
                        nextLevel.push(node.right);
                    }
                } else {
                    if (node.right != null) {
                        nextLevel.push(node.right);
                    }
                    if (node.left != null) {
                        nextLevel.push(node.left);
                    }
                }
            }

            result.add(currLevelResult);
            tmp = currLevel;
            currLevel = nextLevel;
            nextLevel = tmp;
            normalOrder = !normalOrder;
        }

        return result;

    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)