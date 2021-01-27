# 等价二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/identical-binary-tree/?utm_source=sc-github-wzz)
 ## 题目描述
 检查两棵二叉树是否等价。等价的意思是说，首先两棵二叉树必须拥有相同的结构，并且每个对应位置上的节点上的数都相等。
 ### 样例说明
 
 ### 参考代码
 ```cpp
/**
 * Definition of TreeNode:
 * class TreeNode {
 * public:
 *     int val;
 *     TreeNode *left, *right;
 *     TreeNode(int val) {
 *         this->val = val;
 *         this->left = this->right = NULL;
 *     }
 * }
 */
class Solution {
public:
    /**
     * @aaram a, b, the root of binary trees.
     * @return true if they are identical, or false.
     */
    bool isIdentical(TreeNode* a, TreeNode* b) {
        // Write your code here
        if(!a && !b)
            return true;
        else if(!a && b)
            return false;
        else if(a && !b)
            return false;
        else {
            if(a->val != b->val)
                return false;
            else
                return isIdentical(a->left, b->left) && isIdentical(a->right, b->right);
        }
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)