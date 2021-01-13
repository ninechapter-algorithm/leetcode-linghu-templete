# 二叉树的路径和 III
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-path-sum-iii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树和一个目标值，找到二叉树上所有的和为该目标值的路径。路径可以从二叉树的任意节点出发，任意节点结束。

 ### 样例说明
 **样例 1:**

```plain
输入：{1,2,3,4},6
输出：[[2, 4],[2, 1, 3],[3, 1, 2],[4, 2]]
解释：
该树如下：
    1
   / \
  2   3
 /
4
```

**样例 2:**

```plain
输入：{1,2,3,4},3
输出：[[1,2],[2,1],[3]]
解释：
该树如下：
    1
   / \
  2   3
 /
4
```
 ### 参考代码
 使用dfs搜索的办法进行查找，可以进行相关的嵌套，从而达到结果
```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public int val;
 *     public ParentTreeNode parent, left, right;
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @param target an integer
     * @return all valid paths
     */
    public List<List<Integer>> binaryTreePathSum3(ParentTreeNode root, int target) {
        // Write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        dfs(root, target, results);
        return results;
    }
    
    public void dfs(ParentTreeNode root, int target, List<List<Integer>> results) {
        if (root == null)
            return;

        List<Integer> path = new ArrayList<Integer>();
        findSum(root, null, target, path, results);

        dfs(root.left, target, results);
        dfs(root.right, target, results);
    }

    public void findSum(ParentTreeNode root, ParentTreeNode father, int target,
                 List<Integer> path, List<List<Integer>> results) {
        path.add(root.val);
        target -= root.val;
        
        if (target == 0) {
            ArrayList<Integer> tmp = new ArrayList<Integer>();
            Collections.addAll(tmp,  new  Integer[path.size()]); 
            Collections.copy(tmp, path); 
            results.add(tmp);
        }

        if (root.parent != null && root.parent != father)
            findSum(root.parent, root, target, path, results);

        if (root.left != null && root.left  != father)
            findSum(root.left, root, target, path, results);

        if (root.right != null && root.right != father)
            findSum(root.right, root, target, path, results);

        path.remove(path.size() - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)