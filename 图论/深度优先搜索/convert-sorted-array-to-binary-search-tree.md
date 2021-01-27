# 有序数组转换为二叉搜索树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/convert-sorted-array-to-binary-search-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数组，其中元素按升序排序，将其转换为高度平衡的BST。

对于这个问题，高度平衡的二叉树被定义为二叉树，其中每个节点的两个子树的深度从不相差超过1。
 ### 样例说明
 **样例 1:**
```
输入: [-10,-3,0,5,9],
输出: [0,-3,9,-10,#,5],
解释:
针对该数组的其中一个解为 [0,-3,9,-10,null,5], 其对应的平衡BST树如下:
      0
     / \
   -3   9
   /   /
 -10  5
```


**样例 2:**
```
输入: [1,3]
输出: [3,1]
解释:
针对该数组的其中一个解为 [3,1], 其对应的平衡BST树如下:
  3
 / 
1   
```



 ### 参考代码
 考点：
* 递归
* BST

题解：每次选择一个区间的中点作为当前区间的根，然后对左右子树依次构造。
```java
public class Solution {
    private TreeNode buildTree(int[] num, int start, int end) {
        if (start > end) {
            return null;
        }

        TreeNode node = new TreeNode(num[(start + end) / 2]);
        node.left = buildTree(num, start, (start + end) / 2 - 1);
        node.right = buildTree(num, (start + end) / 2 + 1, end);
        return node;
    }

    public TreeNode sortedArrayToBST(int[] num) {
        if (num == null) {
            return null;
        }
        return buildTree(num, 0, num.length - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)