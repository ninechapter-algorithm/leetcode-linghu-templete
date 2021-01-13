# 二叉查找树迭代器
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/binary-search-tree-iterator/?utm_source=sc-github-wzz)
 ## 题目描述
 设计实现一个带有下列属性的二叉查找树的迭代器：
next()返回BST中下一个最小的元素
- 元素按照递增的顺序被访问（比如中序遍历）
- `next()`和`hasNext()`的询问操作要求**均摊**时间复杂度是O(*1*)
 ### 样例说明
 **样例 1:**

```
输入：{10,1,11,#,6,#,12}
输出：[1, 6, 10, 11, 12]
解释：
二叉查找树如下 :
  10
  /\
 1 11
  \  \
   6  12
可以返回二叉查找树的中序遍历 [1, 6, 10, 11, 12]
```

**样例 2:**

``` 
输入：{2,1,3}
输出：[1,2,3]
解释：
二叉查找树如下 :
  2
 / \
1   3
可以返回二叉查找树的中序遍历 [1,2,3]
```
 ### 参考代码
 这是一个非常通用的利用 stack 进行 Binary Tree Iterator 的写法。

stack 中保存一路走到当前节点的所有节点，stack.peek() 一直指向 iterator 指向的当前节点。
因此判断有没有下一个，只需要判断 stack 是否为空
获得下一个值，只需要返回 stack.peek() 的值，并将 stack 进行相应的变化，挪到下一个点。

挪到下一个点的算法如下：

1. 如果当前点存在右子树，那么就是右子树中“一路向西”最左边的那个点
2. 如果当前点不存在右子树，则是走到当前点的路径中，第一个左拐的点

访问所有节点用时O(n)，所以均摊下来访问每个节点的时间复杂度时O(1)
```java
public class BSTIterator {
    private Stack<TreeNode> stack = new Stack<>();
    
    // @param root: The root of binary tree.
    public BSTIterator(TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }

    //@return: True if there has next node, or false
    public boolean hasNext() {
        return !stack.isEmpty();
    }
    
    //@return: return next node
    public TreeNode next() {
        TreeNode curt = stack.peek();
        TreeNode node = curt;
        
        // move to the next node
        if (node.right == null) {
            node = stack.pop();
            while (!stack.isEmpty() && stack.peek().right == node) {
                node = stack.pop();
            }
        } else {
            node = node.right;
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
        }
        
        return curt;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)