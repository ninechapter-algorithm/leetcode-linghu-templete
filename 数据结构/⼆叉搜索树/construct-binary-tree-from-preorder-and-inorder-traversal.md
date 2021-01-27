# 前序遍历和中序遍历树构造二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/construct-binary-tree-from-preorder-and-inorder-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 根据前序遍历和中序遍历树构造二叉树.
 ### 样例说明
 **样例 1:**
```
输入：[],[]
输出：{}
解释：
二叉树为空
```
**样例 2:**
```
输入：[2,1,3],[1,2,3]
输出：{2,1,3}
解释：
二叉树如下
  2
 / \
1   3
```

 ### 参考代码
 Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

前序的第一个为根，在中序中找到根的位置。
中序中根的左右两边即为左右子树的中序遍历。同时可知左子树的大小size-left。
前序中根接下来的size-left个是左子树的前序遍历。
由此可以递归处理左右子树。
```java
public class Solution {
    private int findPosition(int[] arr, int start, int end, int key) {
        int i;
        for (i = start; i <= end; i++) {
            if (arr[i] == key) {
                return i;
            }
        }
        return -1;
    }

    private TreeNode myBuildTree(int[] inorder, int instart, int inend,
            int[] preorder, int prestart, int preend) {
        if (instart > inend) {
            return null;
        }

        TreeNode root = new TreeNode(preorder[prestart]);
        int position = findPosition(inorder, instart, inend, preorder[prestart]);

        root.left = myBuildTree(inorder, instart, position - 1,
                preorder, prestart + 1, prestart + position - instart);
        root.right = myBuildTree(inorder, position + 1, inend,
                preorder, position - inend + preend + 1, preend);
        return root;
    }

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (inorder.length != preorder.length) {
            return null;
        }
        return myBuildTree(inorder, 0, inorder.length - 1, preorder, 0, preorder.length - 1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)