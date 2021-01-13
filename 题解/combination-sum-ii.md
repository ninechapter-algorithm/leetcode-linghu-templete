# 数字组合 II
 > 题目来源: [LintCode 算法题库](https://www.lintcode.com/problem/combination-sum-ii/?utm_source=sc-github-wzz)
 ## 题目描述
 给定一个数组 `num` 和一个整数 `target`. 找到 `num` 中所有的数字之和为 `target` 的组合.
 ### 样例说明
 **样例 1:**

```
输入: num = [7,1,2,5,1,6,10], target = 8
输出: [[1,1,6],[1,2,5],[1,7],[2,6]]
```

**样例 2:**

```
输入: num = [1,1,1], target = 2
输出: [[1,1]]
解释: 解集不能包含重复的组合
```
 ### 参考代码
 使用回溯法搜索所有可能的组合. 很基础的题目, 有多种不同的写法, 再次不多赘述.

有一个显而易见的小优化: 我们在搜索的过程中会记录已经选择的数字的和, 如果这个和超过了 target, 停止搜索. 除此之外还有很多可以优化的细节, 慢慢探索吧!

另外, 这个题目还可以有非递归的形式: 用一个整型的 `num.length` 个二进制位表示一个组合, 第 i 位为 1 表示这个组合内含有 `num[i]`. 这样可以从0自增这个整型来达到枚举所有组合的效果. 避免了递归的开销 (但是也不一定比递归快, 因为递归可以有优化, 而这样枚举就只能老老实实把所有的组合都查看一遍)
```java
public class Solution {
    /**
     * @param num: Given the candidate numbers
     * @param target: Given the target number
     * @return: All the combinations that sum to target
     */
    public List<List<Integer>> combinationSum2(int[] candidates,
            int target) {
        List<List<Integer>> results = new ArrayList<>();
        if (candidates == null || candidates.length == 0) {
            return results;
        }

        Arrays.sort(candidates);
        List<Integer> combination = new ArrayList<Integer>();
        helper(candidates, 0, combination, target, results);

        return results;
    }

    private void helper(int[] candidates,
                        int startIndex,
                        List<Integer> combination,
                        int target,
                        List<List<Integer>> results) {
        if (target == 0) {
            results.add(new ArrayList<Integer>(combination));
            return;
        }

        for (int i = startIndex; i < candidates.length; i++) {
            if (i != startIndex && candidates[i] == candidates[i - 1]) {
                continue;
            }
            if (target < candidates[i]) {
                break;
            }
            combination.add(candidates[i]);
            helper(candidates, i + 1, combination, target - candidates[i], results);
            combination.remove(combination.size() - 1);
        }
    }
}
```
 更多题解请参考: [LintCode 提供 2000+ 算法题和名企阶梯训练](https://www.lintcode.com/problem/?utm_source=sc-github-wzz)