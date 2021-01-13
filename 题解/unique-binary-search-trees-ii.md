# 不同的二叉查找树 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/unique-binary-search-trees-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p><span style="color: rgb(113, 113, 113); font-family: 'Open Sans', 'Helvetica Neue', Helvetica, Arial, sans-serif;">给出n，生成所有由1...n为节点组成的不同的二叉查找树</span><br></p>
 ### 样例说明
 **样例 1:**

```
输入:3
输出:
    1         3     3       2    1
     \       /     /       / \    \
      3     2     1       1   3    2
     /     /       \                \
    2     1         2                3
```
 ### 参考代码
 Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example,
Given n = 3, your program should return all 5 unique BST's shown below.

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```java
public class Solution {
    public ArrayList<TreeNode> generateTrees(int n) {
        return generate(1, n);
    }
    
    private ArrayList<TreeNode> generate(int start, int end){
        ArrayList<TreeNode> rst = new ArrayList<TreeNode>();   
    
        if(start > end){
            rst.add(null);
            return rst;
        }
     
        for(int i=start; i<=end; i++){
            ArrayList<TreeNode> left = generate(start, i-1);
            ArrayList<TreeNode> right = generate(i+1, end);
            for(TreeNode l: left){
                for(TreeNode r: right){
                    // should new a root here because it need to 
                    // be different for each tree
                    TreeNode root = new TreeNode(i);  
                    root.left = l;
                    root.right = r;
                    rst.add(root);
                }
            }
        }
        return rst;
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)