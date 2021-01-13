# 最小子树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/minimum-subtree/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树, 找到和为最小的子树, 返回其根节点。输入输出数据范围都在int内。
 ### 样例说明
 **样例 1:**

```
输入:
{1,-5,2,1,2,-4,-5}
输出:1
说明
这棵树如下所示：
     1
   /   \
 -5     2
 / \   /  \
1   2 -4  -5 
整颗树的和是最小的，所以返回根节点1.
```

**样例 2:**

```
输入:
{1}
输出:1
说明:
这棵树如下所示：
   1
这棵树只有整体这一个子树，所以返回1.
```


 ### 参考代码
 使用 Divide Conquer + Traverse 的方法。
```
[[python]]
class Solution:
    def findSubtree(self, root):
        self.minimum_weight = float('inf')
    	self.minimum_subtree_root = None
        self.getTreeSum(root)

        return self.minimum_subtree_root

    # 得到 root 为根的二叉树的所有节点之和
    # 顺便打个擂台求出 minimum subtree
    def getTreeSum(self, root):
        if root is None:
            return 0

        left_weight = self.getTreeSum(root.left)
        right_weight = self.getTreeSum(root.right)
        root_weight = left_weight + right_weight + root.val
        
        if root_weight < self.minimum_weight:
            self.minimum_weight = root_weight
            self.minimum_subtree_root = root

        return root_weight
[[java]]
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
    private int minSum;
    private TreeNode minRoot;
    
    /**
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
    public TreeNode findSubtree(TreeNode root) {
        minSum = Integer.MAX_VALUE;
        minRoot = null;
        getSum(root);
        return minRoot;
    }
    
    private int getSum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int sum = getSum(root.left) + getSum(root.right) + root.val;
        if (sum < minSum) {
            minSum = sum;
            minRoot = root;
        }
        
        return sum;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)