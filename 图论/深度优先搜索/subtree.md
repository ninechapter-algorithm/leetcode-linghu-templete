# 子树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subtree/?utm_source=sc-github-wzz)
 ## 题目描述
 有两个不同大小的二叉树： `T1` 有上百万的节点； `T2` 有好几百的节点。请设计一种算法，判定 `T2` 是否为 `T1`的子树。

 ### 样例说明
 **样例 1：**
```
输入：{1,2,3,#,#,4},{3,4}
输出：true
解释：
下面的例子中 T2 是 T1 的子树：

           1                3
          / \              / 
    T1 = 2   3      T2 =  4
            /
           4
```
**样例 2：**
```
输入：{1,2,3,#,#,4},{3,#,4}
输出：false
解释：
下面的例子中 T2 不是 T1 的子树：

           1               3
          / \               \
    T1 = 2   3       T2 =    4
            /
           4
```
 ### 参考代码
 考点：
* 搜索遍历

题解：首先判断两树根节点开始是否相同，如果不相同，就从T1的子树和T2当前节点递归搜索。
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
     * @param T1, T2: The roots of binary tree.
     * @return: True if T2 is a subtree of T1, or false.
     */
    public boolean isSubtree(TreeNode T1, TreeNode T2) {
        if (T2 == null) {
            return true;
        }
        if (T1 == null) {
            return false;
        }
        
        if (isEqual(T1, T2)) {
            return true;
        }
        if (isSubtree(T1.left, T2) || isSubtree(T1.right, T2)) {
            return true;
        }
        return false;
    }
    
    private boolean isEqual(TreeNode T1, TreeNode T2) {
        if (T1 == null || T2 == null) {
            return T1 == T2;
        }
        if (T1.val != T2.val) {
            return false;
        }
        return isEqual(T1.left, T2.left) && isEqual(T1.right, T2.right);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)