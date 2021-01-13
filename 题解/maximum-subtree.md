# 最大子树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/maximum-subtree/?utm_source=sc-github-wzz)
 ## 题目描述
 给你一棵二叉树，找二叉树中的一棵子树，他的所有节点之和最大。

返回这棵子树的根节点。
 ### 样例说明
 **样例 1:**

```
输入:
{1,-5,2,0,3,-4,-5}
输出:3
说明
这棵树如下所示：
     1
   /   \
 -5     2
 / \   /  \
0   3 -4  -5
以3为根的子树（只有3一个节点）的和是最大的，所以返回3。
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
 以每个点为根节点root（即每一个子树），找到左子树的节点x和与右子树的节点和y。如果root.val + x.val + y.val > 当前已知最大值，就更新答案。
```python
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {int} the maximum weight node
    import sys
    maximum_weight = 0
    result = None

    def findSubtree(self, root):
        # Write your code here
        self.helper(root)

        return self.result

    def helper(self, root):
        if root is None:
            return 0

        left_weight = self.helper(root.left)
        right_weight = self.helper(root.right)
        
        if left_weight + right_weight + root.val >= self.maximum_weight or self.result is None:
            self.maximum_weight = left_weight + right_weight + root.val
            self.result = root

        return left_weight + right_weight + root.val
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)