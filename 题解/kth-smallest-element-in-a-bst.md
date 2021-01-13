# BST中第K小的元素
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/kth-smallest-element-in-a-bst/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉搜索树，写一个 `KthSmallest` 函数来找到其中第 K 小的元素。
 ### 样例说明
 **样例 1:**
```
输入：{1,#,2},2
输出：2
解释：
	1
	 \
	  2
第二小的元素是2。
```


**样例 2:**
```
输入：{2,1,3},1
输出：1
解释：
  2
 / \
1   3
第一小的元素是1。
```
 ### 参考代码
 时间复杂度 $O(n)$ 最好最坏都是。
算法思想类似于 Quick Select。
这个算法的好处是，如果多次查询的话，给每个节点统计儿子个数这个过程只需要做一次。查询可以很快。
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
     * @param root: the given BST
     * @param k: the given k
     * @return: the kth smallest element in BST
     */
    public int kthSmallest(TreeNode root, int k) {
        Map<TreeNode, Integer> numOfChildren = new HashMap<>();
        countNodes(root, numOfChildren);
        return quickSelectOnTree(root, k, numOfChildren);
    }
    
    private int countNodes(TreeNode root, Map<TreeNode, Integer> numOfChildren) {
        if (root == null) {
            return 0;
        }
        
        int left = countNodes(root.left, numOfChildren);
        int right = countNodes(root.right, numOfChildren);
        numOfChildren.put(root, left + right + 1);
        return left + right + 1;
    }
    
    private int quickSelectOnTree(TreeNode root, int k, Map<TreeNode, Integer> numOfChildren) {
        if (root == null) {
            return -1;
        }
        
        int left = root.left == null ? 0 : numOfChildren.get(root.left);
        if (left >= k) {
            return quickSelectOnTree(root.left, k, numOfChildren);
        }
        if (left + 1 == k) {
            return root.val;
        }
        
        return quickSelectOnTree(root.right, k - left - 1, numOfChildren);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)