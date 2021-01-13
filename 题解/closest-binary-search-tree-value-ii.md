# 二叉搜索树中最接近的值 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/closest-binary-search-tree-value-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一棵非空二叉搜索树以及一个target值，找到 BST 中最接近给定值的 `k` 个数。
 ### 样例说明
 **样例 1:**
```
输入:
{1}
0.000000
1
输出:
[1]
解释：
二叉树 {1}，表示如下的树结构：
 1
```

**样例 2:**
```
输入:
{3,1,4,#,2}
0.275000
2
输出:
[1,2]
解释：
二叉树 {3,1,4,#,2}，表示如下的树结构：
  3
 /  \
1    4
 \
  2
```
 ### 参考代码
 最优算法，时间复杂度 $O(k + logn)$，空间复杂度 $O(logn)$

实现如下的子函数：

1. getStack() => 在假装插入 target 的时候，看看一路走过的节点都是哪些，放到 stack 里，用于 iterate
2. moveUpper(stack) => 根据 stack，挪动到 next node
3. moveLower(stack) => 根据 stack, 挪动到 prev node

有了这些函数之后，就可以把整个树当作一个数组一样来处理，只不过每次 i++ 的时候要用 moveUpper，i--的时候要用 moveLower
```
[[java]]
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> values = new ArrayList<>();
        
        if (k == 0 || root == null) {
            return values;
        }
        
        Stack<TreeNode> lowerStack = getStack(root, target);
        Stack<TreeNode> upperStack = new Stack<>();
        upperStack.addAll(lowerStack);
        if (target < lowerStack.peek().val) {
            moveLower(lowerStack);
        } else {
            moveUpper(upperStack);
        }
        
        for (int i = 0; i < k; i++) {
            if (lowerStack.isEmpty() ||
                   !upperStack.isEmpty() && target - lowerStack.peek().val > upperStack.peek().val - target) {
                values.add(upperStack.peek().val);
                moveUpper(upperStack);
            } else {
                values.add(lowerStack.peek().val);
                moveLower(lowerStack);
            }
        }

        return values;
    }
    
    private Stack<TreeNode> getStack(TreeNode root, double target) {
        Stack<TreeNode> stack = new Stack<>();
        
        while (root != null) {
            stack.push(root);
            
            if (target < root.val) {
                root = root.left;
            } else {
                root = root.right;
            }
        }
        
        return stack;
    }
    
    public void moveUpper(Stack<TreeNode> stack) {
        TreeNode node = stack.peek();
        if (node.right == null) {
            node = stack.pop();
            while (!stack.isEmpty() && stack.peek().right == node) {
                node = stack.pop();
            }
            return;
        }
        
        node = node.right;
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
    }
    
    public void moveLower(Stack<TreeNode> stack) {
        TreeNode node = stack.peek();
        if (node.left == null) {
            node = stack.pop();
            while (!stack.isEmpty() && stack.peek().left == node) {
                node = stack.pop();
            }
            return;
        }
        
        node = node.left;
        while (node != null) {
            stack.push(node);
            node = node.right;
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)