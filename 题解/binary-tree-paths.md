# 二叉树的所有路径
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-paths/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树，找出从根节点到叶子节点的所有路径。
 ### 样例说明
 **样例 1:**
```
输入：{1,2,3,#,5}
输出：["1->2->5","1->3"]
解释：
   1
 /   \
2     3
 \
  5
```
**样例 2:**
```
输入：{1,2}
输出：["1->2"]
解释：
   1
 /   
2     
```
 ### 参考代码
 使用分治算法(Divide Conquer)
```java
// version 1: Divide Conquer
public class Solution {
    /**
     * @param root the root of the binary tree
     * @return all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> paths = new ArrayList<>();
        if (root == null) {
            return paths;
        }
        
        List<String> leftPaths = binaryTreePaths(root.left);
        List<String> rightPaths = binaryTreePaths(root.right);
        for (String path : leftPaths) {
            paths.add(root.val + "->" + path);
        }
        for (String path : rightPaths) {
            paths.add(root.val + "->" + path);
        }
        
        // root is a leaf
        if (paths.size() == 0) {
            paths.add("" + root.val);
        }
        
        return paths;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)