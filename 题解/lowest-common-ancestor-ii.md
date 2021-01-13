# 最近公共祖先 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/lowest-common-ancestor-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给一棵二叉树和二叉树中的两个节点，找到这两个节点的最近公共祖先`LCA`。

两个节点的最近公共祖先，是指两个节点的所有父亲节点中（包括这两个节点），离这两个节点最近的公共的节点。

每个节点除了左右儿子指针以外，还包含一个父亲指针`parent`，指向自己的父亲。
 ### 样例说明
 **样例 1:**
```
输入：{4,3,7,#,#,5,6},3,5
输出：4
解释：
     4
     / \
    3   7
       / \
      5   6
LCA(3, 5) = 4
```
**样例 2:**
```
输入：{4,3,7,#,#,5,6},5,6
输出：7
解释：
      4
     / \
    3   7
       / \
      5   6
LCA(5, 6) = 7
```
 ### 参考代码
 将两个结点移动到相同的高度，然后同时向上移动，直到移动到相同的点
```
[[java]]
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */
public class Solution {
    /**
     * @param root: The root of the tree
     * @param A, B: Two node in the tree
     * @return: The lowest common ancestor of A and B
     */
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root,
                                                 ParentTreeNode A,
                                                 ParentTreeNode B) {
        ArrayList<ParentTreeNode> pathA = getPath2Root(A);
        ArrayList<ParentTreeNode> pathB = getPath2Root(B);
        
        int indexA = pathA.size() - 1;
        int indexB = pathB.size() - 1;
        
        ParentTreeNode lowestAncestor = null;
        while (indexA >= 0 && indexB >= 0) {
            if (pathA.get(indexA) != pathB.get(indexB)) {
                break;
            }
            lowestAncestor = pathA.get(indexA);
            indexA--;
            indexB--;
        }
        
        return lowestAncestor;
    }
    
    private ArrayList<ParentTreeNode> getPath2Root(ParentTreeNode node) {
        ArrayList<ParentTreeNode> path = new ArrayList<>();
        while (node != null) {
            path.add(node);
            node = node.parent;
        }
        return path;
    }
}
[[python]]
"""
Definition of ParentTreeNode:
class ParentTreeNode:
    def __init__(self, val):
        self.val = val
        self.parent, self.left, self.right = None, None, None
"""
class Solution:
    """
    @param root: The root of the tree
    @param A and B: Two node in the tree
    @return: The lowest common ancestor of A and B
    """ 
    def lowestCommonAncestorII(self, root, A, B):
        visited = set()
        while A is not root:
            visited.add(A)
            A = A.parent

        while B is not root:
            if B in visited:
                return B
            B = B.parent

        return root
[[c++]]
/**
 * Definition of ParentTreeNode:
 * class ParentTreeNode {
 * public:
 *     int val;
 *     ParentTreeNode *parent, *left, *right;
 * }
 */
class Solution {
public:
    /**
     * @param root: The root of the tree
     * @param A, B: Two node in the tree
     * @return: The lowest common ancestor of A and B
     */
    int Atop, Btop, top;
    ParentTreeNode *a[100000], *b[100000], *ans[100000];
    bool find;
    void inorder(ParentTreeNode *node, ParentTreeNode *A, int flag) { 
        if (find==true)
            return;
        if (node == NULL)
            return;
        ans[++top] = node;
        if (A == node) {
            find = true;
            if (flag == 0) {
                Atop = top;
                for (int i = 1; i <= top; ++i)
                    a[i] = ans[i];
            } else {
                Btop = top;
                for (int i = 1; i <= top; ++i)
                    b[i] = ans[i];
            }
            return;
        }

        inorder(node->left, A, flag);
        if (find) return;
            
        inorder(node->right, A, flag);
        if (find) return;
          
        top --;
        
    }

    ParentTreeNode *lowestCommonAncestorII(ParentTreeNode *root,
                                           ParentTreeNode *A,
                                           ParentTreeNode *B) {
        // Write your code here
        top = 0; find = false;
        inorder(root, A, 0);

        top = 0; find = false;
        inorder(root, B, 1);
  
        Atop = min(Atop, Btop);
        Btop = Atop;

        while (a[Atop] != b[Btop]) {
            Atop --;
            Btop --;
        }
        return a[Atop];
    }
};
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)