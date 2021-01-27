# 路径总和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/path-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

 ### 样例说明
 **样例 1:**
```
输入: root = {5,4,8,11,#,13,4,7,2,#,#,5,1}, sum = 22
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
输出: [[5,4,11,2],[5,8,4,5]]
解释:
两条路径之和为 22：
5 + 4 + 11 + 2 = 22
5 + 8 + 4 + 5 = 22
```
**样例 2:**
```
输入: root = {10,6,7,5,2,1,8,#,9}, sum = 18
              10
             /  \
            6    7
          /  \   / \
          5  2   1  8
           \ 
            9 
输出: [[10,6,2],[10,7,1]]
解释:
两条路径之和为 18：
10 + 6 + 2 = 18
10 + 7 + 1 = 18
```
 ### 参考代码
 Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:
Given the below binary tree and sum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
return
[
   [5,4,11,2],
   [5,8,4,5]
]
```java
public class Solution {
    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        ArrayList<ArrayList<Integer>> rst = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> solution = new ArrayList<Integer>();

        findSum(rst, solution, root, sum);
        return rst;
    }

    private void findSum(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> solution, TreeNode root, int sum){
        if (root == null) {
            return;
        }

        sum -= root.val;

        if (root.left == null && root.right == null) {
            if (sum == 0){
                solution.add(root.val);
                result.add(new ArrayList<Integer>(solution));
                solution.remove(solution.size()-1);
            }
            return;
        }

        solution.add(root.val);
        findSum(result, solution, root.left, sum);
        findSum(result, solution, root.right, sum);
        solution.remove(solution.size()-1);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)