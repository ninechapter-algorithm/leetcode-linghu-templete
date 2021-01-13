# k数和 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/k-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 <p>给定n个不同的正整数，整数k（1<span style="line-height: 1.42857143;">&lt;=&nbsp;</span><span style="line-height: 1.42857143;">k &lt;= n）以及一个目标数字。　　　　</span></p><p>在这n个数里面找出K个数，使得这K个数的和等于目标数字，你需要找出所有满足要求的方案。</p>
 ### 样例说明
 **样例 1:**

```
输入: [1,2,3,4], k = 2, target = 5
输出:  [[1,4],[2,3]]
```

**样例 2:**

```
输入: [1,3,4,6], k = 3, target = 8
输出:  [[1,3,4]]	
```
 ### 参考代码
 使用九章算法班上讲的模板
```
[[python]]
class Solution:
    """
    @param: A: an integer array
    @param: k: a postive integer <= length(A)
    @param: targer: an integer
    @return: A list of lists of integer
    """
    def kSumII(self, A, k, target):
        A = sorted(A)
        subsets = []
        self.dfs(A, 0, k, target, [], subsets)
        return subsets
        
    def dfs(self, A, index, k, target, subset, subsets):
        if k == 0 and target == 0:
            subsets.append(list(subset))
            return
        
        if k == 0 or target <= 0:
            return
        
        for i in range(index, len(A)):
            subset.append(A[i])
            self.dfs(A, i + 1, k - 1, target - A[i], subset, subsets)
            subset.pop()

[[java]]
public class Solution {
    /*
     * @param A: an integer array
     * @param k: a postive integer <= length(A)
     * @param target: an integer
     * @return: A list of lists of integer
     */
    public List<List<Integer>> kSumII(int[] A, int k, int target) {
        Arrays.sort(A);
        List<List<Integer>> subsets = new ArrayList();
        
        dfs(A, 0, k, target, new ArrayList<Integer>(), subsets);
        
        return subsets;
    }
    
    private void dfs(int[] A, int index, int k, int target,
                     List<Integer> subset,
                     List<List<Integer>> subsets) {
        if (k == 0 && target == 0) {
            subsets.add(new ArrayList<Integer>(subset));
            return;
        }
        if (k == 0 || target <= 0) {
            return;
        }
        
        for (int i = index; i < A.length; i++) {
            subset.add(A[i]);
            dfs(A, i + 1, k - 1, target - A[i], subset, subsets);
            subset.remove(subset.size() - 1);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)