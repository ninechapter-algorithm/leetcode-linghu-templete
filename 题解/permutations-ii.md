# 带重复元素的排列
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/permutations-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给出一个具有重复数字的列表，找出列表所有**不同**的排列。
 ### 样例说明
 **样例 1：**
```
输入：[1,1]
输出：
[
  [1,1]
]
```
**样例 2：**
```
输入：[1,2,2]
输出：
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```
 ### 参考代码
 使用排列式深度优先搜索算法。

和没有重复元素的 Permutation 一题相比，只加了两句话：

1. Arrays.sort(nums)  // 排序这样所有重复的数
2. if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) { continue; } // 跳过会造成重复的情况
```java
public class Solution {
    /*
     * @param :  A list of integers
     * @return: A list of unique permutations
     */
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> results = new ArrayList<>();
        if (nums == null) {
            return results;
        }
        
        Arrays.sort(nums);
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
            if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) {
                continue;
            }
            
            permutation.add(nums[i]);
            visited[i] = true;
            dfs(nums, visited, permutation, results);
            visited[i] = false;
            permutation.remove(permutation.size() - 1);
        }
    }
 };
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)