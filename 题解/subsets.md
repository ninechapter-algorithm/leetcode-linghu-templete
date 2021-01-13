# 子集
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/subsets/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个含不同整数的集合，返回其所有的子集。
 ### 样例说明
 **样例 1：**
```
输入：[0]
输出：
[
  [],
  [0]
]
```
**样例 2：**
```
输入：[1,2,3]
输出：
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
 ### 参考代码
 使用组合类搜索的专用深度优先搜索算法。
一层一层的决策每个数要不要放到最后的集合里。
```java
public class Solution {
    /**
     * @param nums: A set of numbers
     * @return: A list of lists
     */
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        Arrays.sort(nums);
        dfs(nums, 0, new ArrayList<Integer>(), results);
        return results;
    }
    
    // 1. 递归的定义
    // 以 subset 开头的，配上 nums 以 index 开始的数所有组合放到 results 里
    private void dfs(int[] nums,
                     int index,
                     List<Integer> subset,
                     List<List<Integer>> results) {
        // 3. 递归的出口
        if (index == nums.length) {
            results.add(new ArrayList<Integer>(subset));
            return;
        }
        
        // 2. 递归的拆解
        // (如何进入下一层)
        
        // 选了 nums[index]
        subset.add(nums[index]);
        dfs(nums, index + 1, subset, results);
        
        // 不选 nums[index]
        subset.remove(subset.size() - 1);
        dfs(nums, index + 1, subset, results);
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)