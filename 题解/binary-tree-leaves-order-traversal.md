# 二叉树叶子顺序遍历
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-leaves-order-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树，像这样收集树节点：收集并移除所有叶子，重复，直到树为空。
 ### 样例说明
 
 ### 参考代码
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
     * @param root the root of binary tree
     * @return collect and remove all leaves
     */
    public List<List<Integer>> findLeaves(TreeNode root) {
        // Write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        dfs(root, results);
        return results;
    }

    int dfs(TreeNode root, List<List<Integer>> results) {
        if (root == null) {
            return 0;
        }
        int level = Math.max(dfs(root.left, results), dfs(root.right, results)) + 1;
        int size = results.size();
        if (level > size) {
            results.add(new ArrayList<Integer>());
        }
        results.get(level - 1).add(root.val);
        return level;
    }   
}

// version: 高频题班
public class Solution {
    /**
     * @param root the root of binary tree
     * @return collect and remove all leaves
     */

    int dfs(TreeNode cur, Map<Integer, List<Integer>> depth) {
        if (cur == null) {
            return 0;
        }
        int d = Math.max(dfs(cur.left, depth), dfs(cur.right, depth)) + 1;

        depth.putIfAbsent(d, new ArrayList<>());
        depth.get(d).add(cur.val);
        return d;
    }

    public List<List<Integer>> findLeaves(TreeNode root) {
        // Write your code here
        List<List<Integer>> ans = new ArrayList<>();

        Map<Integer, List<Integer>> depth = new HashMap<>();
        int max_depth = dfs(root, depth);

        for (int i = 1; i <= max_depth; i++) {
            ans.add(depth.get(i));
        }
        return ans;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)