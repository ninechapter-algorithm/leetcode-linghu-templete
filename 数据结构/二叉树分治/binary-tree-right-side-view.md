# 二叉树的右视图
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-tree-right-side-view/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。
 ### 样例说明
 **样例1**

```
输入: {1,2,3,#,5,#,4}
输出: [1,3,4]
说明:
   1            
 /   \
2     3         
 \     \
  5     4       
```

**样例2**

```plain
输入: {1,2,3}
输出: [1,3]
说明:
   1            
 /   \
2     3        
```


 ### 参考代码
 dfs暴力即可。
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private void dfs(HashMap<Integer, Integer> depthToValue, TreeNode node, int depth) {
        if (node == null) {
            return;
        }
        
        depthToValue.put(depth, node.val);
        dfs(depthToValue, node.left, depth + 1);
        dfs(depthToValue, node.right, depth + 1);
    }
    
    public List<Integer> rightSideView(TreeNode root) {
        HashMap<Integer, Integer> depthToValue = new HashMap<Integer, Integer>();
        dfs(depthToValue, root, 1);
        
        int depth = 1;
        List<Integer> result = new ArrayList<Integer>();
        while (depthToValue.containsKey(depth)) {
            result.add(depthToValue.get(depth));
            depth++;
        }
        return result;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)