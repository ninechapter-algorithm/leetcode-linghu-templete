# 具有最大平均数的子树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subtree-with-maximum-average/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树，找到有最大平均值的子树。返回子树的根结点。
 ### 样例说明
 **样例1**

```
输入：
{1,-5,11,1,2,4,-2}
输出：11
说明:
这棵树如下所示：
     1
   /   \
 -5     11
 / \   /  \
1   2 4    -2 
11子树的平均值是4.333，为最大的。
```

**样例2**

```
输入：
{1,-5,11}
输出：11
说明:
     1
   /   \
 -5     11
1,-5,11 三棵子树的平均值分别是 2.333,-5,11。因此11才是最大的
```
 ### 参考代码
 因为需要求平均数，所以要记录节点和以及接节点个数
自定义一个ResultType，记录节点和以及接节点个数
分治法计算每一颗子树的平均值，打擂台求出最大平均数的子树
```java
// version 1: Traverse + Divide Conquer
public class Solution {
    private class ResultType {
        public int sum, size;
        public ResultType(int sum, int size) {
            this.sum = sum;
            this.size = size;
        }
    }
    
    private TreeNode subtree = null;
    private ResultType subtreeResult = null;
    
    /**
     * @param root the root of binary tree
     * @return the root of the maximum average of subtree
     */
    public TreeNode findSubtree2(TreeNode root) {
        helper(root);
        return subtree;
    }
    
    private ResultType helper(TreeNode root) {
        if (root == null) {
            return new ResultType(0, 0);
        }
        // 分治法计算左右子树的平均值
        ResultType left = helper(root.left);
        ResultType right = helper(root.right);
        // 当前subtree的结果是左右两颗子树的和的平均值加上自身
        ResultType result = new ResultType(
            left.sum + right.sum + root.val,
            left.size + right.size + 1
        );
        // 打擂台比较得到最大平均值的子树
        if (subtree == null ||
            subtreeResult.sum * result.size < result.sum * subtreeResult.size
        ) {
            subtree = root;
            subtreeResult = result;
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)