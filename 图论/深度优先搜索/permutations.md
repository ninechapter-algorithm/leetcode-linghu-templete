# 全排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/permutations/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数字列表，返回其所有可能的排列。
 ### 样例说明
 **样例 1：**
```
输入：[1]
输出：
[
  [1]
]
```
**样例 2：**
```
输入：[1,2,3]
输出：
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
 ### 参考代码
 使用深度优先搜索算法。
使用 visited 数组记录某个数是否被放到 permutation 里了。
```
[[java]]
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null) {
            return results;
        }
        
        dfs(nums, new boolean[nums.length], new ArrayList<Integer>(), results);
        
        return results;
    }
    
    private void dfs(int[] nums,
                     boolean[] visited,
                     List<Integer> permutation,
                     List<List<Integer>> results) {
        if (nums.length == permutation.size()) {
            results.add(new ArrayList<Integer>(permutation));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            permutation.add(nums[i]);
            visited[i] = true;
            dfs(nums, visited, permutation, results);
            visited[i] = false;
            permutation.remove(permutation.size() - 1);
        }
    }
}
[[python]]
class Solution:
    """
    @param: nums: A list of integers.
    @return: A list of permutations.
    """
    def permute(self, nums):
        if not nums:
            return [[]]
            
        permutations = []
        self.dfs(nums, [], set(), permutations)
        return permutations
        
    def dfs(self, nums, permutation, visited, permutations):
        if len(nums) == len(permutation):
            permutations.append(list(permutation))
            return
        
        for num in nums:
            if num in visited:
                continue
            permutation.append(num)
            visited.add(num)
            self.dfs(nums, permutation, visited, permutations)
            visited.remove(num)
            permutation.pop()
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)