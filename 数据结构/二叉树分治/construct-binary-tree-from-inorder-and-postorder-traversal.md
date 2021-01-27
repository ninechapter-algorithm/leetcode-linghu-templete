# 中序遍历和后序遍历树构造二叉树
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/construct-binary-tree-from-inorder-and-postorder-traversal/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>根据中序遍历和后序遍历树构造二叉树</p>
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
输入：[1,2,3],[1,3,2]
输出：{2,1,3}
解释：
二叉树如下
  2
 / \
1   3
```


 ### 参考代码
 根据当前后续序列的最后一个结点，在对应的中序遍历中找到位置，然后相同的方法，递归左右子树即可。
```cpp
#include <vector>
#include "lintcode.h"
#include <algorithm>
using namespace std;

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
    /**
     *@param inorder : A list of integers that inorder traversal of a tree
     *@param postorder : A list of integers that postorder traversal of a tree
     *@return : Root of a tree
     */
public:
    typedef vector<int>::iterator Iter;
    TreeNode *buildTree(vector<int> &inorder, vector<int> &postorder) {
        // write your code here
        if (inorder.size() == 0)
            return NULL;
        return buildTreeRecur(inorder.begin(), inorder.end(), postorder.begin(), 
        postorder.end());
    }
    TreeNode *buildTreeRecur(Iter istart, Iter iend, Iter pstart, Iter pend)
    {
        if(istart == iend)return NULL;
        int rootval = *(pend-1);
        Iter iterroot = find(istart, iend, rootval);
        TreeNode *res = new TreeNode(rootval);
        res->left = buildTreeRecur(istart, iterroot, pstart, pstart+(iterroot-istart));
        res->right = buildTreeRecur(iterroot+1, iend, pstart+(iterroot-istart), pend-1);
        return res;
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)