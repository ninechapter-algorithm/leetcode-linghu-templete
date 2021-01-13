# 组合
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/combinations/?utm_source=sc-github-wzz)
 ## 题目描述
 给定两个整数 `n` 和 `k`. 返回从 `1, 2, ... , n` 中选出 `k` 个数的所有可能的组合.
 ### 样例说明
 **样例 1:**

```
输入: n = 4, k = 2
输出: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
```

**样例 2:**

```
输入: n = 4, k = 1
输出: [[1],[2],[3],[4]]
```
 ### 参考代码
 Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> rst = new ArrayList<List<Integer>>();
        List<Integer> solution = new ArrayList<Integer>();
        
        helper(rst, solution, n, k, 1);
        return rst;
    }
    
    private void helper(List<List<Integer>> rst, List<Integer> solution, 
        int n, int k, int start) {
        if (solution.size() == k){
            rst.add(new ArrayList(solution));
            return;
        }
        
        for(int i = start; i<= n; i++){
            solution.add(i);
            
            // the new start should be after the next number after i
            helper(rst, solution, n, k, i + 1); 
            solution.remove(solution.size() - 1);
        }
    }
}

```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)